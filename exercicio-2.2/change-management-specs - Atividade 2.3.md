# Change Management para Specs em Implementação

**Versão:** 1.0  
**Data:** 18/06/2026  
**Owner:** Tech Lead + Product Specialist  
**Efetivo a partir de:** Sprint 1 (quando implementation começar)

---

## 1. Cenário: Por que specs mudam durante implementação?

### Cenários Reais (Todos Esperados)

**Cenário 1: Ambiguidade descoberta durante coding**
```
Dia 5 (NOVA-1.2 em andamento):
  Dev Sênior implementa AC3: "chunks ≤ 1500 tokens"
  Realiza: não é claro se 1500 é unicode chars, UTF-8 bytes, ou OpenAI tokens
  Impacto: teste falhando, ambiguidade causa retrabalho
  Ação: Spec precisa ser refinada (AC3 agora diz "OpenAI token count via tiktoken")
```

**Cenário 2: Descoberta técnica muda a abordagem**
```
Dia 3 (NOVA-1.4 - embedding):
  Dev descobre: Azure OpenAI embeddings estão deprecated em favor de text-embedding-3-small
  Impacto: plan.md dizia "usaremos embedding v1", mas v1 será removido
  Ação: Plan precisa ser atualizado (stack agora é "text-embedding-3-small, deprecated v1")
```

**Cenário 3: Cliente pede ajuste durante implementation**
```
Dia 7 (NOVA-1.6 - integration):
  Cliente: "Espera, preciso também de busca por data (não só similaridade)"
  Impacto: novo requirement que não estava em requirements.md
  Ação: Spec precisa evoluir (novo AC adicionado a requirements.md)
```

**Cenário 4: QA descobre cenário não testado**
```
Dia 8 (GATE-4 code review):
  QA: "Quando documento é > 100K tokens, o chunker trata corretamente?"
  AC mencionava, mas não testado explicitamente
  Ação: Tasks precisa de novo subtask (NOVA-1.7.1 "test > 100K token edge case")
```

**Cenário 5: Produção revela problema de performance**
```
Pós-deploy (monitoring em produção):
  Latência P95 degradou de 1.8s para 2.5s durante peak hours
  Impacto: plan.md dizia "< 2s SLA" mas não se sustenta em produção
  Ação: Spec precisa ser revisitada (otimização nova task, ou reavaliar SLA)
```

---

## 2. Tipos de Mudanças & Severidade

### Matriz de Mudanças

| Tipo | Severidade | Quem Pode Alterar? | Quem Aprova? | SLA | Exemplo |
|------|-----------|-------------------|--------------|-----|---------|
| **AC Refinement** | 🟢 Baixa | Dev + Tech Lead | Tech Lead | 4h | AC3: "1500 tokens" → "1500 OpenAI tokens via tiktoken" |
| **AC Reestimativa** | 🟡 Média | Dev + Tech Lead | Tech Lead | 24h | NOVA-1.2: 8pt → 10pt (mais complexity descoberta) |
| **Stack Adjustment** | 🟡 Média | Tech Lead | Tech Lead + CTO | 24h | plan.md: embedding v1 → text-embedding-3-small |
| **New Requirement** | 🟠 Alta | Product Specialist | Product Lead + Tech Lead | 48h | Cliente quer busca por data, não só similaridade |
| **Scope Creep** | 🔴 Crítica | — (escalação obrigatória) | CTO + Client | 72h | "Enquanto estamos aqui, vocês poderiam adicionar..." |
| **SLA Violation** | 🔴 Crítica | Tech Lead | Tech Lead + Product Lead | 48h | Latência P95 2.5s em produção, plan dizia < 2s |

---

## 3. Quem Pode Alterar Spec?

### Matriz de Autorização

| Papel | requirements.md | plan.md | tasks.md | Limite | Requer Aprovação? |
|-------|-----------------|---------|----------|--------|------------------|
| **Product Specialist** | ✅ Pode escrever | ❌ Não | ❌ Não | Sem client request | Tech Lead |
| **Tech Lead** | ⚠️ Refinement só | ✅ Pode escrever | ✅ Pode refinar | Sem scope creep | CTO se > 24h |
| **Dev Sênior** | ❌ Não | ⚠️ Refinement só | ✅ Pode refinar | AC clarity | Tech Lead (4h) |
| **Dev Pleno** | ❌ Não | ❌ Não | ⚠️ AC clarification | Menor ambiguidade | Tech Lead (4h) |
| **QA** | ❌ Não | ❌ Não | ⚠️ Edge case AC | Testes descobertos | Tech Lead (4h) |
| **CTO** | ✅ Veto/escalação | ✅ Veto/escalação | ✅ Veto/escalação | Sem limite | N/A (autoridade máxima) |

**Regra Geral:** Nunca altera spec sem aprovação de Tech Lead (ou escalação para CTO).

---

## 4. Processo de Change Management (Por Tipo)

### Tipo 1️⃣: AC Refinement (🟢 Baixa Severidade)

**Descrição:** AC precisa de clarificação, não muda intenção original.

**Exemplo:**
```
AC3 antes: "chunks ≤ 1500 tokens"
AC3 depois: "chunks ≤ 1500 tokens (OpenAI token count via tiktoken library)"

Intenção original: "chunks não muito grandes"
Mudança: "apenas clareza de como contar"
```

**Processo:**

1. **Dev/QA Identifica** (when coding/testing)
   ```
   Slack message @tech-lead:
   "NOVA-1.2 AC3 ambígua. Atualmente diz '≤ 1500 tokens' mas qual token count?
    OpenAI? UTF-8? Sugiro: 'OpenAI token count via tiktoken'.
    Posso prosseguir assumindo isso?"
   ```

2. **Tech Lead Approves** (SLA: 4h)
   ```
   Response (within 4h):
   "✅ Aprovado. AC3 agora: 'Chunks ≤ 1500 tokens (OpenAI via tiktoken)'.
    Commitei em tasks.md. Prossiga com teste."
   ```

3. **Atualiza Spec**
   ```
   /specs/pipeline-ingestao/tasks.md
   
   NOVA-1.2 AC3 (v1.1):
     "Chunks ≤ 1500 tokens (OpenAI token count via tiktoken library)"
   ```

4. **Changelog Updated**
   ```
   > **Changelog:**
   > - v1.1 (2026-06-25 10h) AC3 token count explicit, 
   >   discovered during NOVA-1.2 impl, approved by Tech Lead
   > - v1.0 (2026-06-21) initial
   ```

5. **Commit**
   ```
   git commit -m "update: pipeline-ingestao/tasks v1.1 — AC3 token count clarity
   
   Issue: Dev realizou ambiguidade em AC3 durante NOVA-1.2 coding
   Solution: Explicitamente mencionar OpenAI token count (tiktoken)
   Approved: Tech Lead, 2026-06-25 10h"
   ```

6. **Task Continues**
   ```
   NOVA-1.2 continua com AC refinado
   Teste atualizado para validar "OpenAI token count"
   Sem impacto em outras tasks (AC ainda é ≤ 1500, só mais claro)
   ```

**SLA:** 4 horas (decisão rápida, dev bloqueado)  
**Escalação:** Se Tech Lead não responder em 4h, Dev assume interpretation e continua (documenta assumption)

---

### Tipo 2️⃣: AC Reestimativa (🟡 Média Severidade)

**Descrição:** Complexity de task mudou descoberta durante implementação.

**Exemplo:**
```
NOVA-1.2 antes: 8 points (Dev achava que chunking era simples)
NOVA-1.2 depois: 10 points (descoberto: overlap handling é complexo)

Intenção original: "decompor documento em chunks"
Mudança: "esforço estimado mudou"
```

**Processo:**

1. **Dev Identifica** (quando coding)
   ```
   Slack @tech-lead:
   "NOVA-1.2 está mais complexo que 8pt.
    Overlap handling com 20% é tricky, preciso ajustar chunker múltiplas vezes.
    Estimo 10pt agora. Posso rever estimate?"
   ```

2. **Tech Lead Reviews** (SLA: 24h)
   ```
   Tech Lead analisa:
   - Código atual
   - Teste complexidade
   - Impacto em outras tasks
   
   Response (within 24h):
   "✅ Concorda. NOVA-1.2 agora 10pt (de 8pt).
    Velocidade do sprint não muda: ainda 37pt total (compensado).
    Prossiga."
   ```

3. **Atualiza Spec**
   ```
   /specs/pipeline-ingestao/tasks.md
   
   NOVA-1.2 (v1.1):
   Description: PDF/DOCX extraction + chunking with 20% overlap
   Points: 10 (updated from 8)
   ```

4. **Changelog Updated**
   ```
   > **Changelog:**
   > - v1.1 (2026-06-25) NOVA-1.2 reestimated from 8pt to 10pt,
   >   overlap complexity discovered during impl, approved by Tech Lead
   > - v1.0 (2026-06-21) initial
   ```

5. **Azure DevOps Updated**
   ```
   Work Item: NOVA-1.2
   Field "Story Points": 8 → 10
   Comment: "Reestimated during implementation. 
             Overlap handling more complex than anticipated.
             Approved by Tech Lead, 2026-06-25"
   ```

6. **Impact Assessment**
   ```
   Total sprint velocity: 37pt (was 8, now 10 = +2)
   Still fits sprint? YES (total 37pt fits 40pt capacity)
   Other tasks affected? NO (independent)
   Velocity projection: on track
   ```

**SLA:** 24 horas (permite discussion)  
**Escalação:** Se novo total > 40pt (sprint capacity), escalação para Delivery Manager (pode estender sprint ou mover tasks)

---

### Tipo 3️⃣: Stack Adjustment (🟡 Média Severidade)

**Descrição:** Decisão técnica muda (new library, deprecated API, etc).

**Exemplo:**
```
plan.md antes: "embedding: Azure OpenAI text-embedding-ada-002 (soon deprecated)"
plan.md depois: "embedding: Azure OpenAI text-embedding-3-small (recommended)"

Intenção original: "usar Azure OpenAI embeddings"
Mudança: "qual modelo específico"
```

**Processo:**

1. **Tech Lead Identifica** (pode ser dev comunicando)
   ```
   Slack @tech-lead:
   "NOVA-1.4 (embedding): Azure OpenAI just announced ada-002 is deprecated.
    Recomenda text-embedding-3-small. Preciso atualizar plan.md?"
   ```

2. **Tech Lead Decides** (pode ser rápido ou escalado)
   ```
   Análise:
   - Impacto: mudança simples (API é compatível)
   - Risco: nenhum (new model é melhor)
   - Esforço: zero (apenas update plan.md)
   
   Se LOW risk: Tech Lead aprova sozinho
   Se HIGH risk: escalação para CTO
   ```

3. **Atualiza Spec**
   ```
   /specs/pipeline-ingestao/plan.md
   
   ## Stack
   - Embedding: Azure OpenAI text-embedding-3-small 
     (replaced deprecated ada-002, 2026-06-25)
   ```

4. **Changelog Updated**
   ```
   > **Changelog:**
   > - v1.1 (2026-06-25) embedding model updated to text-embedding-3-small
   >   (ada-002 deprecated by Azure OpenAI), no breaking change, approved Tech Lead
   > - v1.0 (2026-06-20) initial
   ```

5. **Tasks Impact Check**
   ```
   NOVA-1.4 (embedding + indexing):
   - Precisa mudar? Código é genérico, funciona com qualquer modelo
   - Teste precisa mudar? Sim, mock agora usa text-embedding-3-small
   - Reestimativa? Não (mudança 0 pontos, só update)
   ```

6. **Commit**
   ```
   git commit -m "update: pipeline-ingestao/plan v1.1 — embedding model update
   
   Change: text-embedding-ada-002 → text-embedding-3-small
   Reason: ada-002 deprecated by Azure OpenAI
   Impact: No breaking change, API compatible
   Approved: Tech Lead, 2026-06-25"
   ```

**SLA:** 24 horas (mas geralmente decisão rápida)  
**Escalação:** Se impacto em outras tasks ou risco alto → CTO

---

### Tipo 4️⃣: New Requirement (🟠 Alta Severidade)

**Descrição:** Novo requirement que não estava em requirements.md original.

**Exemplo:**
```
Cliente: "Ah sim, além de busca por similaridade, 
         vocês poderiam filtrar por data de documento?
         Importante para compliance."

Status: Em implementação (NOVA-1.6 já foi feito)
Impacto: 1+ novo AC, possivelmente novo task
```

**Processo:**

1. **Product Specialist Identifica** (usually client feedback)
   ```
   Slack @tech-lead @delivery-manager:
   "Cliente (compliance team) pede feature nova:
    Busca por data de documento, não só similaridade.
    Isso era scope? Preciso adicionar requirements.md?"
   ```

2. **Tech Lead + Delivery Manager Analyze** (SLA: 48h)
   ```
   Questions:
   - Era scope original? Não (não em requirements.md v1.0)
   - É urgente? Sim (compliance)
   - Esforço? ~3-5 pontos (filter logic)
   - Timing? Sprint 1 ainda em implementação (NOVA-1.6)
   
   Decision options:
   A) Add como novo AC para requirements.md, estender sprint
   B) Defer para Sprint 2 (query-endpoint module)
   C) Escalation ao cliente (scope vs timing tradeoff)
   ```

3. **Escalation Path**
   ```
   Tech Lead propõe:
   "Option A: adiciona AC novo a requirements.md v1.1
             (search by document date), nova task NOVA-1.8
             Sprint 1 estende 2 dias, entrega 30/06 → 02/07"
   
   Delivery Manager + Product Lead decidem:
   "Aprovado Option A. Cliente quer compliance feature.
    Estendemos Sprint 1 até 02/07. Comunicado ao cliente."
   ```

4. **Atualiza Specs**
   ```
   /specs/pipeline-ingestao/requirements.md
   
   US-4 (novo): Filtrar resultados por data de documento
   AC1: Query pode incluir filtro "after:2024-01-01"
   AC2: Chunks indexados com metadata "document_date"
   AC3: Resultado retorna documentos apenas nessa data range
   ```

5. **New Task Created**
   ```
   /specs/pipeline-ingestao/tasks.md
   
   NOVA-1.8 (novo): Add document date filtering
   Points: 5
   Depends: NOVA-1.7 (tests)
   AC: (todos testáveis)
   ```

6. **Changelogs Updated**
   ```
   requirements.md v1.1:
   > - v1.1 (2026-06-25) Added US-4: document date filtering,
   >   client compliance requirement, approved by Product Lead + Tech Lead
   
   tasks.md v1.1:
   > - v1.1 (2026-06-25) Added NOVA-1.8: document date filter (5pt),
   >   new user story from client, impacts timeline
   ```

7. **Impact on Sprint**
   ```
   Original: 37pt, due 30/06
   New: 37pt + 5pt = 42pt, due 02/07 (extend 2 days)
   
   Timeline updated:
   - NOVA-1.7 (tests): 21/06-26/06 (unchanged)
   - NOVA-1.8 (new): 26/06-30/06 (added)
   - GATE-4/5/6: 26/06-02/07 (extended)
   
   Team informed: meeting/slack
   ```

8. **Commits**
   ```
   git commit -m "feat: add document date filtering requirement
   
   User story: US-4 (client compliance request)
   Tasks: NOVA-1.8 (5pt, date filtering logic)
   Impact: Sprint 1 extended to 02/07 (3 extra days)
   Approved: Product Lead + Tech Lead, 2026-06-25"
   ```

**SLA:** 48 horas (complex decision, may require client discussion)  
**Escalation:** If scope creep or high impact → CTO + Client

---

### Tipo 5️⃣: Scope Creep (🔴 Crítica - ESCALATION OBRIGATÓRIA)

**Descrição:** Mudança que não é refinement, nem client request estruturado. É "Enquanto estamos aqui, vocês poderiam...?"

**Exemplo:**
```
Dev: "Enquanto a gente tá indexando documentos, 
     vocês poderiam adicionar suporte para OCR de PDFs escaneados?
     Seria útil para compliance."

Avaliação:
- Escopo? Não (original excluía OCR)
- Esforço? 20+ pontos (OCR é complexo)
- Timing? Sprint 1 em andamento
```

**Processo (HARD STOP):**

1. **VETO Imediato** (quando identificado)
   ```
   Tech Lead:
   "🚫 SCOPE CREEP ALERT
   
   Proposta: suporte OCR para PDFs escaneados
   Status: NÃO é parte de requirements v1.0
   Esforço: ~20pt, fora de escopo
   Timeline: comprometeria Sprint 1
   
   Ação: REJEITADO, escalação obrigatória para CTO + Product Lead"
   ```

2. **Escalation ao CTO + Product Lead** (imediato)
   ```
   Slack @cto @product-lead:
   "⚠️ Scope creep detected.
    Proposta: OCR support, 20pt esforço, out of scope
    Impact: se aceito, Sprint 1 extends +1 week
    
    Decision needed: approve feature, defer to future sprint, ou rejeitar?"
   ```

3. **CTO Decision** (SLA: 24h, pode ser urgente)
   ```
   CTO analysis:
   - Is it feature creep? YES (not in requirements v1.0)
   - Is it urgent? NO (mentioned casually)
   - Can we afford it? NO (Sprint 1 timeline already tight)
   
   Decision: REJECTED
   
   Response:
   "🚫 Feature rejected. Out of scope for Sprint 1.
    If client needs OCR later, create new epic (Sprint 6+).
    Do not add to requirements v1.0."
   ```

4. **Document Rejection** (for future reference)
   ```
   /docs/scope-creep-log.md
   
   2026-06-25: OCR Support Request
   Status: REJECTED (out of scope)
   Reason: 20pt effort, not in requirements v1.0, no client request
   Decision maker: CTO
   Deferred to: Future sprint (if client asks)
   ```

5. **Communicate to Team**
   ```
   Slack @team:
   "⚠️ OCR support request was out of scope and rejected.
    Requirements v1.0 explicitly excludes OCR.
    If client needs this, we'll discuss in future sprint.
    Focus on Sprint 1 tasks: NOVA-1.1 until 1.8"
   ```

**SLA:** 24 hours (must be quick to prevent rework)  
**Escalation:** Mandatory to CTO + Product Lead  
**Outcome:** Almost always REJECTED (protect scope)

---

### Tipo 6️⃣: SLA Violation (🔴 Crítica - POST-DEPLOYMENT)

**Descrição:** Spec prometia algo, mas produção viola SLA.

**Exemplo:**
```
plan.md: "Latência P95 < 2s (SLA)"
Produção: Latência P95 = 2.5s durante peak hours

Status: Deploy GATE-6 passou, está em produção
Impacto: SLA violado, precisa de otimização
```

**Processo:**

1. **Monitoring Detects** (automation)
   ```
   Alert triggers:
   "⚠️ Latency P95 > 2s (current: 2.5s)
    SLA violation: plan.md says < 2s
    Escalate to Tech Lead"
   ```

2. **Tech Lead + Delivery Manager + Product Lead Meeting** (ASAP)
   ```
   Emergency sync:
   
   Tech Lead: "P95 latência violou SLA (2.5s vs 2s esperado).
              Provável causa: cache hits baixo durante peak.
              Opções:
              A) Otimizar (implement caching) → +1 week
              B) Renegotiate SLA (novo target: 2.5s) → client approval needed
              C) Hybrid (cache + relax SLA)"
   
   Product Lead: "Cliente SLA é Gold tier = 2s max.
                 Violação pode ter penalties.
                 Preciso comunicar cliente ASAP."
   
   Delivery Manager: "Timeline? Sprint 2 começa amanhã.
                     Se otimiza, atrasa sprint 2.
                     Se renegocia, preciso client agreement."
   ```

3. **Atualiza Spec com Análise**
   ```
   /specs/pipeline-ingestao/plan.md v1.2
   
   ## Performance Analysis (Post-Deploy)
   
   Observed Latency:
   - P95: 2.5s (expected: < 2s)
   - Peak hours: 3.1s (high variance)
   
   Root cause: Embedding cache has 15% hit rate
               (expected: > 80%)
   
   Options:
   A) Implement Redis cache for embeddings
      Effort: 8-10pt
      Timeline: +1 week
      Expected result: P95 < 1.5s
   
   B) Relax SLA to 2.5s (renegotiate with client)
      Effort: 0pt
      Timeline: immediate (client approval)
      Expected result: compliant with revised SLA
   
   C) Hybrid: Cache + SLA relaxation
      Effort: 4-5pt
      Timeline: +3 days
      Expected result: P95 < 2.0s
   ```

4. **Client Communication** (Product Lead)
   ```
   Email to client (compliance):
   
   "Subject: Performance Optimization - Pipeline Ingestão
   
   We've detected that latency in peak hours is reaching 2.5s 
   (SLA target: 2.0s).
   
   Root cause: Embedding cache efficiency during high load.
   
   Proposed solutions:
   A) Optimize caching (1 week, recommended)
   B) Adjust SLA to 2.5s (immediate)
   C) Hybrid approach (3 days)
   
   Please advise preference. We'll prioritize accordingly."
   ```

5. **Decision + Plan**
   ```
   Client chooses Option A: Optimize caching
   
   Sprint 2 updated:
   - NOVA-2.X moved to lower priority
   - NOVA-1.9 created: "Implement Redis caching for embeddings"
   - Timeline: 3 days, 8pt
   - Owner: Dev Sênior
   ```

6. **Spec Updated**
   ```
   /specs/pipeline-ingestao/plan.md v1.2
   
   > **Changelog:**
   > - v1.2 (2026-07-02) Post-deploy performance analysis,
   >   SLA violation detected (P95 2.5s), optimization planned,
   >   NOVA-1.9 created for caching, approved by Tech Lead + Product Lead
   > - v1.1 (2026-06-25) document date filtering
   > - v1.0 (2026-06-20) initial
   ```

7. **Commits**
   ```
   git commit -m "fix: add caching optimization for embedding latency
   
   Issue: Post-deploy monitoring shows P95 latency 2.5s (SLA: < 2s)
   Root cause: Low cache hit rate (~15%) during peak hours
   Solution: Implement Redis caching for embeddings (NOVA-1.9)
   Timeline: +1 week, expected P95 < 1.5s after deployment
   Approved: Tech Lead + Product Lead, client agreement"
   ```

**SLA:** 48 hours (urgent but needs analysis + client discussion)  
**Escalation:** Immediate to CTO + Product Lead + Client  
**Recovery:** New task created, timeline adjusted

---

## 5. Impact Analysis Template

Quando uma mudança é proposta, **sempre fazer Impact Analysis**:

```
CHANGE IMPACT ANALYSIS TEMPLATE

Change: [descrição]
Severity: 🟢 / 🟡 / 🟠 / 🔴
Proposed by: [pessoa]
Date: [data]

TASKS AFFECTED:
  ☐ NOVA-1.1: [ ] No impact / [ ] Minor / [ ] Major
     Reason: [se houver impacto]
     
  ☐ NOVA-1.2: [ ] No impact / [ ] Minor / [ ] Major
     Reason: [se houver impacto]
  
  [... list all tasks ...]

TIMELINE IMPACT:
  Original deadline: [data]
  Impact: [ ] None / [ ] +1 day / [ ] +2-3 days / [ ] +1 week+
  Reason: [detalhado]

REWORK REQUIRED:
  [ ] Code: [o quê precisa ser refatorado]
  [ ] Tests: [testes que précisam ser atualizados]
  [ ] Documentation: [specs que précisam mudar]

EFFORT ESTIMATION:
  Refactor: [Xpt]
  Test: [Ypt]
  Documentation: [Zpt]
  Total: [X+Y+Z]pt

APPROVAL NEEDED FROM:
  [ ] Tech Lead
  [ ] Product Lead
  [ ] Client (se scope)
  [ ] CTO (se crítico)

RECOMMENDATION:
  [ ] Approve and proceed (with rework plan)
  [ ] Defer to next sprint
  [ ] Reject (out of scope)
  [ ] Escalate to CTO
```

---

## 6. Exemplo Real: Change from Start to Finish

### Change Scenario: AC Refinement

**Timeline:**

```
Jun 25, 10h:
  Dev Sênior (coding NOVA-1.2): "AC3 é ambígua"
  
Jun 25, 10h:
  Slack @tech-lead: "[CHANGE REQUEST] NOVA-1.2 AC3 refinement needed"
  
Jun 25, 10:30h:
  Tech Lead reviews: "AC3 precisa especificar token counting method"
  
Jun 25, 11h:
  Tech Lead aprova: "✅ AC3 agora: 'OpenAI token count (tiktoken)'"
  
Jun 25, 11h:
  tasks.md updated locally
  Changelog: v1.0 → v1.1 (AC3 clarity)
  
Jun 25, 11h:
  Dev commits: "update: pipeline-ingestao/tasks v1.1 — AC3 token count clarity"
  
Jun 25, 12h:
  Dev continues NOVA-1.2 with refined AC3
  Testes updated para validar token counting
  
Jun 25, 18h:
  NOVA-1.2 completa com AC novo
  No timeline impact (mesma task)
```

### Change Scenario: New Requirement

**Timeline:**

```
Jun 25, 14h:
  Product Specialist: "Cliente pede date filtering, compliance requirement"
  
Jun 25, 14h:
  Slack @tech-lead @delivery-manager: "[CHANGE REQUEST] New requirement: date filtering"
  
Jun 25, 15h:
  Tech Lead analyzes: "Esforço ~5pt, depende NOVA-1.7 (tests)"
  
Jun 25, 16h:
  Delivery Manager: "Sprint 1 = 37pt, +5pt = 42pt (over 40pt capacity).
                   Preciso estender Sprint 1 de 30/06 para 02/07"
  
Jun 25, 17h:
  Product Lead approves: "Cliente quer compliance feature. Extender 2 dias é ok."
  
Jun 26, 09h:
  requirements.md updated: US-4 (date filtering)
  tasks.md updated: NOVA-1.8 (5pt, date filtering task)
  
Jun 26, 09h:
  Commits: "feat: add date filtering requirement (compliance)"
  Changelog: v1.1 → requirements & tasks
  
Jun 26, 10h:
  Meeting com Dev Sênior: "NOVA-1.8 agora faz parte do Sprint 1.
                         Timeline estende para 02/07.
                         Prioridade: NOVA-1.7 → NOVA-1.8 → Gates"
  
Jun 26-30:
  Dev trabalha em NOVA-1.7 (tests)
  
Jul 01:
  Dev começa NOVA-1.8 (date filtering)
  
Jul 02:
  NOVA-1.8 completa
  Gates (code review, tests) começam
  
Jul 02, 17h:
  Sprint 1 "done": requirements v1.1 + plan v1.0 + tasks v1.1
            (with NOVA-1.8 added)
```

---

## 7. Escalation Path

```
CHANGE IDENTIFIED
  │
  ├─→ Is it AC refinement? (Dev + AC clarity only)
  │   └─→ Tech Lead approves (4h SLA)
  │       └─→ Update spec + commit
  │           └─→ Continue task
  │
  ├─→ Is it reestimation? (Task effort changed)
  │   └─→ Tech Lead approves (24h SLA)
  │       └─→ Check sprint capacity
  │       ├─→ Fits? Update Azure DevOps, continue
  │       └─→ Doesn't fit? 
  │           └─→ Escalate to Delivery Manager
  │               └─→ Move task to next sprint or extend current
  │
  ├─→ Is it stack adjustment? (Technical library/API change)
  │   ├─→ Low risk (API compatible)? 
  │   │   └─→ Tech Lead approves alone (24h)
  │   └─→ High risk (breaking change)?
  │       └─→ Escalate to CTO (24h)
  │
  ├─→ Is it new requirement? (Client asked for new feature)
  │   └─→ Product Specialist + Tech Lead + Delivery Manager sync (48h)
  │       ├─→ If low effort (< 3pt): add to current sprint
  │       │   └─→ Extend sprint if over capacity
  │       └─→ If high effort (> 3pt): defer to next sprint
  │           └─→ Log in backlog
  │
  ├─→ Is it scope creep? ("Enquanto estamos aqui...")
  │   └─→ 🚫 REJECT imediato (Tech Lead)
  │       └─→ Escalate to CTO (24h)
  │           └─→ CTO veto
  │
  └─→ Is it SLA violation? (Post-deploy problem)
      └─→ Emergency meeting (Tech Lead + Product Lead + CTO)
          └─→ Impact analysis (48h)
              ├─→ If urgent: create new sprint task
              └─→ If can wait: add to backlog
```

---

## 8. Roles & Permissions

### Change Authority Matrix

| Change Type | Can Propose? | Can Approve? | Can Reject? | Final Say? |
|-------------|-------------|------------|-----------|-----------|
| AC Refinement | Any dev | Tech Lead | Tech Lead | Tech Lead |
| Reestimation | Dev | Tech Lead | Tech Lead | Tech Lead |
| Stack Adjustment (low risk) | Tech Lead | Tech Lead | Tech Lead | Tech Lead |
| Stack Adjustment (high risk) | Tech Lead | CTO | CTO | CTO |
| New Requirement | Product Spec | Product Lead + Tech Lead | Tech Lead | Product Lead |
| Scope Creep | Any | — (auto-reject) | CTO | CTO |
| SLA Violation | Monitoring | Tech Lead + Product Lead | CTO | Product Lead + Client |

---

## 9. Communication Template

### When Proposing a Change

```
[CHANGE REQUEST]

Type: [AC Refinement / Reestimation / Stack Adjustment / New Requirement / ...]
Severity: 🟢 / 🟡 / 🟠 / 🔴

WHAT:
  Description of change needed

WHY:
  Reason for change (discovered during coding, client request, etc)

IMPACT:
  Tasks affected: NOVA-1.X, NOVA-1.Y
  Timeline impact: [none / +X days]
  Effort: [X points if reestimation]
  Rework needed: [Y/N]

APPROVAL NEEDED FROM:
  [ ] Tech Lead
  [ ] Product Lead
  [ ] CTO

RECOMMENDATION:
  Approve / Defer / Reject

[Waiting for approval...]
```

### When Approving a Change

```
✅ [CHANGE APPROVED]

Type: [as proposed]
Approved by: [name]
Date: [timestamp]

DECISION:
  [Approved as proposed / Approved with modifications / Deferred to next sprint]

ACTION:
  1. Update spec (requirements / plan / tasks)
  2. Update changelog (version bump + reason + approval)
  3. Commit to git
  4. Update Azure DevOps if timeline/effort changed
  5. Continue task

[Change now active]
```

---

## 10. Checklist: Before Implementing Change

```
☐ Change documented (what, why, impact)
☐ Correct approval path identified
☐ Approval obtained (all required roles)
☐ Impact analysis complete (tasks, timeline, effort)
☐ Spec updated (requirements/plan/tasks)
☐ Changelog version bumped (v1.0 → v1.1)
☐ Changelog entry explains change + approval
☐ Git commit with clear message
☐ Azure DevOps updated (if timeline/effort changed)
☐ Team informed (if impacts other work)
☐ Rework plan documented (if code/tests change needed)
☐ Continued with updated spec
```

---

## 11. Prevention: How to Avoid Many Changes

### At Spec Creation (Requirements Phase)

**Better Specs = Fewer Changes**

```
☐ Requirements are crystal clear (no vague AC)
☐ Requirements list constraints (not just features)
☐ Requirements reference base documental (chunks, SLAs, PROC-042)
☐ Requirements mention edge cases explicitly
☐ Requirements are reviewed thoroughly BEFORE plan/tasks

If done well: AC refinements drop from 50% to 5%
```

### At Planning Phase (Plan Phase)

**Better Planning = Fewer Surprises**

```
☐ Tech stack fully specified (no "TBD")
☐ Risk matrix covers known unknowns
☐ Golden queries document expected behavior
☐ Latency/throughput/availability constraints documented
☐ Plan is reviewed by both Tech Lead AND Dev Sênior

If done well: Stack adjustments drop from 30% to 5%
             Reestimations drop from 40% to 10%
```

### During Implementation (Implement Phase)

**Pair Programming = Fewer Questions**

```
☐ Dev Sênior does pair programming (especially if ambiguous AC)
☐ Dev raises questions EARLY (not at end of task)
☐ Tech Lead available for quick clarifications (< 4h response)
☐ QA involved early (not just at end)

If done well: AC refinements caught in first 4h of task
             Rework prevented
```

---

## 12. Metrics: Track Change Frequency

**Track to improve process:**

```
Per Sprint:
  - Number of AC refinements (target: < 2)
  - Number of reestimations (target: < 1)
  - Number of new requirements (target: 0 during impl)
  - Number of scope creep attempts (target: 0)
  - Number of SLA violations (target: 0)

Trends:
  Sprint 1: 3 AC refinements (30% change rate = too high)
  Sprint 2: 1 AC refinement (10% change rate = better)
  Sprint 3: 0 AC refinements (0% = good!)
  
  → If refinements decreasing: specs are improving
  → If stable at 0: excellent requirements clarity
  → If increasing: specs are getting worse
```

---

## 13. Próximos Passos

**Before Sprint 1:**

```
☐ Este documento compartilhado com team
☐ Todos entendem: tipos de mudanças + approval paths
☐ Tech Lead + Product Specialist alinhados
☐ Slack channel #change-requests criado (ou using existing #novatech-specs)
☐ Checklist impressa e na parede do escritório
```

**During Sprint 1:**

```
☐ Primeiro change identificado (esperado NOVA-1.2 AC refinement)
☐ Processo executado (Dev propõe, Tech Lead aprova, spec atualiza)
☐ Retrospective: "O processo funcionou? Precisa ajustes?"
```

---

**Fim do Documento.**

Data: 18/06/2026  
Versão: 1.0  
Owner: Tech Lead + Product Specialist  
Próxima revisão: 30/07/2026 (após Sprint 2, com feedback real)

Para questões: Slack #novatech-specs ou @tech-lead
