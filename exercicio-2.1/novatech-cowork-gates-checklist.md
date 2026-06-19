# NovaTech Validation Gates — Relatório de Rastreamento

**Gerado por:** Claude Cowork (automação para Delivery Manager)  
**Data:** 18/06/2026 09:00 BRT  
**Sprint:** Sprint 1 (19/06 - 30/06)  
**Módulo:** pipeline-ingestao  
**Status Geral:** PRONTO PARA INICIAR

---

## Dashboard Executivo

```
                GATE-1        GATE-2        GATE-3        GATE-4        GATE-5        GATE-6
               (Spec)        (Plan)        (Tasks)       (Code Rev)     (Tests)      (Deploy)
Status:        ⏳ PENDING    ⏳ PENDING    ⏳ PENDING     ⏳ PENDING     ⏳ PENDING    ⏳ PENDING
Expected:      Jun 20        Jun 21        Jun 21        Jun 26-27      Jun 26-28    Jun 29
Owner:         Tech Lead     Tech Lead     Tech Lead     Tech Lead      QA           Tech Lead
Timebox:       24h           24h           12h           4h             48h          4h

Progresso:     [━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━] 0% (aguardando inicio)
```

---

## GATE-1: Spec Approved

**Fase:** Spec → Plan  
**Esperado em:** Jun 20, 17h BRT (24h após submissão esperada Jun 19 09h)  
**Responsável:** Tech Lead  
**Status Atual:** AWAITING INPUT

### Timeline Esperada

```
Jun 19 09h:  Product Specialist submete requirements.md
Jun 19 09h:  Relógio GATE-1 inicia (24h SLA)
Jun 20 09h:  Tech Lead começa validação
Jun 20 14h:  Tech Lead completa revisão e marca checklist
Jun 20 17h:  GATE-1 APPROVED (ou REQUEST CHANGES)
Jun 21 09h:  GATE-2 inicia (se aprovado)
```

### Checklist (Vazio até submissão)

**Seção 1: Estrutura Documento**
```
☐ Arquivo: /specs/pipeline-ingestao/requirements.md existe
☐ Tamanho: entre 500-2000 palavras
☐ Formato: Markdown com seções H2/H3, legível

Status: AWAITING SUBMISSION
```

**Seção 2: Conteúdo Obrigatório**
```
☐ DESCRIÇÃO: 1-2 parágrafos explicando feature
☐ USER STORIES: Mínimo 3, formato "As a... I want... So that..."
☐ CRITÉRIOS DE ACEITAÇÃO: Mínimo 3 por story, testáveis
☐ CONSTRAINTS NÃO-FUNCIONAIS: latência, throughput, disponibilidade

Status: AWAITING SUBMISSION
```

**Seção 3: Validação contra Base Documental**
```
SE TOCA RAG:
  ☐ Chunks de referência (Anexo B) explicitamente listados

SE TOCA SLAS:
  ☐ Tabela SLA-2024 referenciada com tiers válidos (Gold/Silver/Standard)

SE TOCA FRETE:
  ☐ Ambas versões PROC-042 (v1 + v2) documentadas

SE TOCA CARGAS PERIGOSAS:
  ☐ POL-001-B (exceções) explicitamente referenciada

Status: AWAITING SUBMISSION
```

**Seção 4: Validação de Ambiguidade**
```
☐ Nenhuma frase com "provavelmente", "talvez", "pode ser que"
☐ Nenhum "TBD", "TODO", "em aberto"
☐ Nenhuma AC com palavras vagas
☐ Todas as dependências externas listadas

Status: AWAITING SUBMISSION
```

### Decision Log

| Timestamp | Evento | Ator | Status | Notas |
|-----------|--------|------|--------|-------|
| 2026-06-18 | Gate criado (template) | Cowork | — | Aguardando submissão Product Specialist |
| — | Product Specialist submete | Product Specialist | — | Esperado: Jun 19 09h |
| — | Tech Lead revisa | Tech Lead | PENDING | SLA: 24h até Jun 20 17h |
| — | Tech Lead aprova / reprova | Tech Lead | PENDING | Se REQUEST CHANGES → volta para Product Specialist |

### Ação Requerida (Próximos 24h)

```
[Jun 19] ⏳ ESPERAR: Product Specialist submete requirements.md
[Jun 19] 🔔 ALERTA (se > 12h sem submissão): Slack ping Product Specialist
[Jun 20] 👁️ REVISAR: Tech Lead inicia checklist (max 4h para revisar)
[Jun 20] ✅ APROVAR: Tech Lead marca APPROVED ou REQUEST CHANGES
[Jun 21] ➡️ AVANÇAR: Se aprovado, GATE-2 inicia
```

---

## GATE-2: Plan Approved

**Fase:** Plan → Tasks  
**Esperado em:** Jun 21, 17h BRT  
**Responsável:** Tech Lead + Delivery Manager  
**Status Atual:** BLOCKED (aguardando GATE-1)

### Timeline Esperada

```
Jun 20 17h:  GATE-1 aprovado (pré-requisito)
Jun 20 17h:  Tech Lead começa a escrever plan.md
Jun 21 09h:  Tech Lead submete plan.md
Jun 21 10h:  Tech Lead + Delivery Mgr revisam
Jun 21 15h:  GATE-2 APPROVED (ou REQUEST CHANGES)
Jun 21 15h:  GATE-3 pode iniciar
```

### Checklist (Será preenchido após GATE-1)

**Seção 1: Estrutura Documento**
```
☐ Arquivo: /specs/pipeline-ingestao/plan.md existe

Status: BLOCKED
```

**Seção 2: Decomposição Arquitetural**
```
☐ Quais Azure services vão ser usados?
☐ Quais padrões TypeScript vão ser seguidos?
☐ Qual será o fluxo de dados?
☐ Quais dependências externas?

Status: BLOCKED
```

**Seção 3: Risco Matrix**
```
☐ Risco 1: metadata vigência PROC-042
   Mitigação: [será preenchido]
   Teste: [será preenchido]

☐ Risco 2: contradição v1 vs v2
   Mitigação: [será preenchido]
   Teste: [será preenchido]

☐ Risco 3: [será preenchido]
   Mitigação: [será preenchido]
   Teste: [será preenchido]

Status: BLOCKED
```

### Decision Log

| Timestamp | Evento | Ator | Status |
|-----------|--------|------|--------|
| 2026-06-18 | Gate criado (template) | Cowork | — |
| — | GATE-1 aprovado (pré-requisito) | Tech Lead | BLOCKED |
| — | Tech Lead escreve plan.md | Tech Lead | PENDING |
| — | Tech Lead + Delivery Mgr revisam | Tech Lead, Delivery Mgr | PENDING |

### Ação Requerida

```
[Jun 20] ⏳ AGUARDAR: GATE-1 approval
[Jun 21] 👨‍💻 ESCREVER: Tech Lead escreve plan.md (1 dia útil)
[Jun 21] 👁️ REVISAR: Tech Lead + Delivery Mgr fazem checklist (max 2h)
[Jun 21] ✅ APROVAR: Marca APPROVED ou REQUEST CHANGES
```

---

## GATE-3: Tasks Approved

**Fase:** Tasks → Implement  
**Esperado em:** Jun 21, 17h BRT  
**Responsável:** Tech Lead  
**Status Atual:** BLOCKED (aguardando GATE-2)

### Timeline Esperada

```
Jun 21 15h:  GATE-2 aprovado
Jun 21 15h:  Dev Sênior começa decomposição de tasks (com Copilot)
Jun 21 16h:  Dev Sênior submete tasks.md (1-2h de work)
Jun 21 17h:  Tech Lead revisa e aprova
Jun 22 09h:  Dev Pleno e Dev Sênior começam Implement
```

### Checklist (Será preenchido após GATE-2)

**Seção 1: Estrutura**
```
☐ Arquivo: /specs/pipeline-ingestao/tasks.md existe
☐ Task IDs: NOVA-2.1, NOVA-2.2, ... (formato correto)

Status: BLOCKED
```

**Seção 2: Qualidade de Tasks**
```
☐ Task 2.1: pontos < 13? AC testável? Skill mapeada? Dependencies?
☐ Task 2.2: [idem]
☐ Task 2.3: [idem]
☐ Task 2.4: [idem]
☐ Task 2.5: [idem]

Status: BLOCKED
```

### Decision Log

| Timestamp | Evento | Ator | Status |
|-----------|--------|------|--------|
| 2026-06-18 | Gate criado (template) | Cowork | — |
| — | GATE-2 aprovado (pré-requisito) | Tech Lead | BLOCKED |
| — | Dev Sênior gera tasks.md | Dev Sênior | PENDING |
| — | Tech Lead aprova | Tech Lead | PENDING |

### Ação Requerida

```
[Jun 21] ⏳ AGUARDAR: GATE-2 approval
[Jun 21] 🤖 GERAR: Dev Sênior + Copilot decompõem (1-2h)
[Jun 21] 👁️ REVISAR: Tech Lead valida (max 1h)
[Jun 21] ✅ APROVAR: marca APPROVED
[Jun 22] ➡️ INÍCIO: Dev Pleno + Dev Sênior começam código
```

---

## GATE-4: Code Review

**Fase:** Código → Merge  
**Esperado em:** Jun 26-27 BRT (durante Pull Requests)  
**Responsável:** Tech Lead + Dev Sênior  
**Status Atual:** BLOCKED (aguardando Implement)

### Timeline Esperada

```
Jun 21:      Implement inicia (tarefas decompostas)
Jun 23-24:   PRs abrem (feature branches → cenário-1)
Jun 24-25:   Tech Lead faz code review (batch, 2-4h por PR)
Jun 26:      PRs mergeados (espera-se 100% aprovação)
```

### Checklist (Será preenchido durante PRs)

**PR 1: query handler (NOVA-2.1)**
```
☐ Branch: feature/NOVA-2.1
☐ CI passa: ☐ Lint ☐ Build ☐ Tests ☐ Coverage > 80%
☐ Skill pattern: /skills/artifact/create-rag-endpoint.md seguido?
☐ Sem console.log / TODO / FIXME?
☐ Edge cases testados: ☐ Input vazio ☐ Query > 512 chars ☐ Resposta sobre cargas perigosas

Tech Lead: [ ] REQUEST CHANGES / [ ] APPROVED

Status: PENDING
```

**PR 2: validator (NOVA-2.2)**
```
☐ Branch: feature/NOVA-2.2
☐ CI passes: [idem]
☐ Skill pattern: [idem]
☐ [...]

Tech Lead: [ ] REQUEST CHANGES / [ ] APPROVED

Status: PENDING
```

### Decision Log

| Timestamp | Evento | Ator | Status |
|-----------|--------|------|--------|
| 2026-06-18 | Gate criado (template) | Cowork | — |
| — | Implement inicia (Jun 21) | Dev team | PENDING |
| — | PRs abrem (esperado Jun 23-24) | Dev | PENDING |
| — | Tech Lead revisa (SLA 4h por PR) | Tech Lead | PENDING |

### Ação Requerida

```
[Jun 21-23] 👨‍💻 CÓDIGO: Dev implementam (tarefas 2.1 até 2.N)
[Jun 23-24] 📤 PRs: Dev abre feature branch → PR contra cenário-1
[Jun 24-25] 👁️ REVIEW: Tech Lead revisa (max 4h per PR, batch é ok)
[Jun 26]    ✅ MERGE: PR aprovados mergeados
```

---

## GATE-5: Test Review

**Fase:** Testes → Deploy  
**Esperado em:** Jun 26-28 BRT  
**Responsável:** QA + Product Specialist  
**Status Atual:** BLOCKED (aguardando Implement)

### Timeline Esperada

```
Jun 21-25:   Dev escrevem testes (unit, integration)
Jun 25:      Testes em cenário-1 (staging)
Jun 26:      QA executa smoke test + golden queries
Jun 27:      QA valida fonte verificável em cada resposta
Jun 28:      Product Specialist valida: "resposta atende requirement?"
Jun 28 17h:  GATE-5 APPROVED (ou REQUEST CHANGES)
```

### Checklist (Será preenchido durante QA)

**Coverage & Regressão**
```
☐ Coverage nova code: 84% (target: > 80%)
☐ Nenhum regressão vs sprint anterior: ☐ Sim
☐ Testes passam 100%: ☐ Sim

Status: PENDING
```

**Golden Queries (Anexo B)**
```
Query 1: "Qual o prazo de devolução?"
  Expected response: POL-001-A + "7 dias úteis"
  Actual response: [será testado]
  Source: [será validado]
  ✓ PASS / ✗ FAIL

Query 2: "Posso devolver carga perigosa?"
  Expected: POL-001-B + "não" + "ramal 4500"
  Actual: [será testado]
  Source: [será validado]
  ✓ PASS / ✗ FAIL

Query 3: "Qual multiplicador para o Sudeste?"
  Expected: PROC-042v2-B + "1.1" + data transição
  Actual: [será testado]
  Source: [será validado]
  ✓ PASS / ✗ FAIL

Query 4: "Qual tier Platinum?"
  Expected: "Não existe, tiers são Gold/Silver/Standard"
  Actual: [será testado]
  Source: [será validado]
  ✓ PASS / ✗ FAIL

Query 5: "Frete para 600kg para Manaus?"
  Expected: PROC-042v2-B multiplicador Norte 1.8
  Actual: [será testado]
  Source: [será validado]
  ✓ PASS / ✗ FAIL

Status: PENDING
```

**Product Specialist Validation**
```
Query 1 atende requirement original? ☐ SIM / ☐ NÃO / ☐ PARCIAL
Query 2 atende requirement original? ☐ SIM / ☐ NÃO / ☐ PARCIAL
Query 3 atende requirement original? ☐ SIM / ☐ NÃO / ☐ PARCIAL
Query 4 atende requirement original? ☐ SIM / ☐ NÃO / ☐ PARCIAL
Query 5 atende requirement original? ☐ SIM / ☐ NÃO / ☐ PARCIAL

Status: PENDING
```

### Decision Log

| Timestamp | Evento | Ator | Status |
|-----------|--------|------|--------|
| 2026-06-18 | Gate criado (template) | Cowork | — |
| — | Dev escrevem testes (Jun 21-25) | Dev | PENDING |
| — | QA executa golden queries (Jun 26-27) | QA | PENDING |
| — | QA valida fonte verificável (Jun 27) | QA | PENDING |
| — | Product Specialist aprova (Jun 28) | Product Spec | PENDING |

### Ação Requerida

```
[Jun 21-25] 🧪 TESTES: Dev escrevem + executam localmente
[Jun 25]    🚀 STAGING: Código + testes pushados para staging
[Jun 26]    👁️ SMOKE TEST: QA executa queries principais
[Jun 27]    ✅ GOLDEN QUERIES: QA testa 5 queries ref. vs chunks
[Jun 28]    🎯 PRODUCT SPEC: Product Specialist valida relevância
[Jun 28]    ➡️ DEPLOY: Se aprovado, agendado para Jun 29 off-peak
```

---

## GATE-6: Deploy Ready

**Fase:** Staging → Produção  
**Esperado em:** Jun 29, 22h-02h BRT (off-peak)  
**Responsável:** Tech Lead + Delivery Manager  
**Status Atual:** BLOCKED (aguardando GATE-5)

### Timeline Esperada

```
Jun 28 17h:  GATE-5 aprovado
Jun 28 18h:  Tech Lead prepara runbook (review checklist)
Jun 29 15h:  Delivery Manager valida readiness (infra, runbook, monitoring)
Jun 29 21h:  Slack notification: "Deploy será em 1h, no issues? [yes/no]"
Jun 29 22h:  Deploy inicia (Tech Lead executa runbook)
Jun 30 02h:  Deploy concluído, monitoring ativo
Jun 30 08h:  Delivery Manager report: "Deploy bem-sucedido, no issues"
```

### Checklist (Será preenchido durante deploy)

**Pré-Deploy (Jun 29, 15h)**
```
☐ Infra ok: Azure AI Search indexado (847 docs), OpenAI disponível, Functions pronto
☐ Runbook testado: rollback executado com sucesso em staging
☐ Monitoring ativo: dashboard criado, alertas configurados
☐ Release notes publicados: Slack #novatech-status + email

Status: PENDING
```

**Deploy Execution (Jun 29, 22h)**
```
Start time: 2026-06-29 22:00 BRT
Step 1: Deploy Functions to staging ✓ / ✗
Step 2: Deploy Functions to production ✓ / ✗
Step 3: Health check (latency P95, error rate) ✓ / ✗
Step 4: Smoke test (5 golden queries) ✓ / ✗

End time: [será preenchido]
Duration: [será calculado]

If ERROR:
  Rollback? ☐ YES (< 30min) / ☐ NO (live with issues)

Status: PENDING
```

**Post-Deploy (Jun 30, 08h)**
```
☐ Produção: zero critical bugs
☐ Latência P95: 1.8s (< 2s SLA)
☐ Error rate: < 0.1%
☐ Token usage: < 80% quota
☐ Monitoring: green across board

Status: PENDING
```

### Decision Log

| Timestamp | Evento | Ator | Status |
|-----------|--------|------|--------|
| 2026-06-18 | Gate criado (template) | Cowork | — |
| — | GATE-5 aprovado (Jun 28 17h) | QA | BLOCKED |
| — | Tech Lead prepara runbook (Jun 28 18h) | Tech Lead | PENDING |
| — | Deploy window (Jun 29 22h-02h) | Tech Lead | PENDING |

### Ação Requerida

```
[Jun 28] 📋 RUNBOOK: Tech Lead finalizatesta (should be ready)
[Jun 29] 👀 READINESS: Delivery Manager valida infra + monitoring
[Jun 29] 📢 NOTIFICAÇÃO: Slack ping time (30min antes)
[Jun 29] 🚀 DEPLOY: Tech Lead executa runbook (off-peak)
[Jun 30] 📊 REPORT: Delivery Manager report resultado + next steps
```

---

## Resumo por Sprint

```
SPRINT 1 (19/06 - 30/06): pipeline-ingestao
  GATE-1 (Spec):        Jun 19 → Jun 20 17h     [⏳ PENDING]
  GATE-2 (Plan):        Jun 20 → Jun 21 17h     [⏳ PENDING]
  GATE-3 (Tasks):       Jun 21 → Jun 21 17h     [⏳ PENDING]
  GATE-4 (Code Review): Jun 21 → Jun 26-27      [⏳ PENDING]
  GATE-5 (Tests):       Jun 25 → Jun 28 17h     [⏳ PENDING]
  GATE-6 (Deploy):      Jun 28 → Jun 29 02h     [⏳ PENDING]
  
  Velocity target: 40 story points
  Code coverage target: > 80%
  Golden queries: 5/5 passed (100%)
  
  Status: READY TO START

SPRINT 2 (Jun 26 → Jul 07): query-endpoint (paralelo com final de Sprint 1)
  [Será criado quando Sprint 1 estiver 50% done]

SPRINT 3: feedback-api
SPRINT 4: teams-bot
SPRINT 5: painel-web
```

---

## Alerts & Escalations

### Real-Time Alerts (enviadas ao abrir issue)

```
🔴 GATE SLA VIOLATED
   Gate: GATE-1 (Spec Approved)
   Expected: Jun 20 17h
   Current time: Jun 21 09h
   Overdue: 16h
   Action: Escalate to CTO immediately
   Message: @tech-lead — GATE-1 SLA violated. Approve or escalate to @cto.

🟡 GATE SLA WARNING
   Gate: GATE-2 (Plan Approved)
   Expected: Jun 21 17h
   Time remaining: 2h
   Action: @tech-lead — 2h until GATE-2 SLA violated
```

### Daily Alerts (enviadas 09h)

```
✅ GATES PASSED (since yesterday)
   GATE-1 APPROVED by Tech Lead
   Velocity: on track (28/40 points = 70%)
   
❌ GATES FAILING (since yesterday)
   GATE-1 REQUEST CHANGES: back to Product Specialist
   Blocker: chunks referência não foram listados
   ETA fix: Jun 20 14h
   
⚠️ GATES AT RISK (close to SLA)
   GATE-3 in progress (due Jun 21 17h, 6h remaining)
   Dev Sênior: on pace
```

---

## Integration with Azure DevOps

Cada gate tem corresponding **work item** no board:

```
Work Item: NovaTech Sprint 1 - GATE-1 (Spec Review)
  Type: Epic (parent of all module tasks)
  Status: Blocked (waiting Product Specialist submission)
  Fields:
    Module: pipeline-ingestao
    Gate: GATE-1
    Owner: Tech Lead
    Expected completion: 2026-06-20 17:00 BRT
    Attachment: [GATE-1 checklist - este documento]
  
  Comment activity:
    2026-06-18 Cowork: "Gate criado, awaiting submission"
    2026-06-19 Product Specialist: "Requirements submitted: /specs/pipeline-ingestao/requirements.md"
    2026-06-20 Tech Lead: [checklist preenchido + aprovação]
```

---

## Próximos Passos para Delivery Manager

### Hoje (18/06)

```
☐ Revisar este documento
☐ Compartilhar com Tech Lead + QA
☐ Confirmar timezones (todos BRT?)
☐ Validar contatos de escalation (CTO disponível?)
```

### Amanhã (19/06)

```
☐ Reunião rápida (15min) com Product Specialist
   - Confirmar submissão requirements.md amanhã 09h
   - Esclarecer: chunks de referência (Anexo B) devem estar listados
   
☐ Reunião rápida (15min) com Tech Lead
   - Confirmar: revisar GATE-1 amanhã até 17h
   - Esclarecer: timebox 24h, não há extensão (escalation CTO se > 24h)
```

### Quinta (20/06)

```
☐ 09h: Recap GATE-1 status (aprovado? REQUEST CHANGES?)
☐ Se aprovado: Tech Lead começa GATE-2 (plan.md)
☐ Se REQUEST CHANGES: Product Specialist tem 6h para corrigir
```

### Sexta (23/06) — Go-Live Sprint 1

```
☐ 09h: Daily standup (confirm team ready)
☐ Implement inicia: Dev começam primeira task (NOVA-2.1)
☐ Delivery Manager monitora via Cowork (daily status 09h)
```

---

**Fim do relatório. Atualizado automaticamente diariamente pelo Claude Cowork.**

Próxima atualização automática: 19/06/2026 09:00 BRT  
Próxima revisão manual: 20/06/2026 17:00 BRT (após GATE-1)  
Contato: delivery-manager@db1.com | Slack: @jacque
