# NovaTech Assistant — Fluxo de Trabalho AI First

**Status:** Operacional  
**Versão:** 2.0 (Ajustado)  
**Efetivo a partir de:** 23/06/2026  
**Propriedade:** Delivery Manager (Jacque) + Tech Lead  
**Próxima revisão:** 30/07/2026 (após 2 sprints)

---

## 1. Princípios Fundamentais

Este fluxo opera sob 4 princípios não-negociáveis:

1. **Papéis × Ferramentas de IA são específicos** — não há "use IA quando necessário", há "Dev Pleno usa Copilot + Claude para debugging, Tech Lead usa Claude para pair review arquitetural"

2. **Validation gates são obrigatórios** — nenhuma fase avança sem aprovação humana explícita. Sem exceções por prazo.

3. **Velocidade é amplificada, não substituída** — IA gera (Copilot código, Claude análise), humano valida (Tech Lead, QA, Product Specialist). Balanceamento 70% IA / 30% validação.

4. **Rastreabilidade é integral** — cada decisão, cada gate, cada reprova é documentada. Não há "confiança cega" em automação.

---

## 2. Estrutura de Fases

O ciclo de desenvolvimento segue **Spec → Plan → Tasks → Implement → Review → Deploy**, com 6 validation gates obrigatórios.

```
┌─────────────────────────────────────────────────────────────────┐
│ SPEC PHASE (2 dias úteis)                                       │
│  Input: Discovery concluído, ADRs finalizadas                  │
│  Owner: Product Specialist (escreve) + Tech Lead (revisa)      │
│  IA tools: Claude Design (mockups), Claude (estruturação)      │
│  Output: /specs/{modulo}/requirements.md                       │
│  ↓ GATE-1: Spec Approved (Tech Lead valida)                    │
├─────────────────────────────────────────────────────────────────┤
│ PLAN PHASE (1 dia útil)                                         │
│  Input: Spec aprovada                                           │
│  Owner: Tech Lead (escreve) + Dev Sênior (revisa)              │
│  IA tools: Claude (arquitetura, risco), GitHub Copilot (ex)    │
│  Output: /specs/{modulo}/plan.md                               │
│  ↓ GATE-2: Plan Approved (Tech Lead + Delivery Mgr)            │
├─────────────────────────────────────────────────────────────────┤
│ TASKS PHASE (1 dia útil)                                        │
│  Input: Plan aprovado                                           │
│  Owner: Dev Sênior (gera com Copilot) + Tech Lead (aprova)     │
│  IA tools: GitHub Copilot (decomposição), Claude (refinamento) │
│  Output: /specs/{modulo}/tasks.md                              │
│  ↓ GATE-3: Tasks Approved (Tech Lead)                          │
├─────────────────────────────────────────────────────────────────┤
│ IMPLEMENT PHASE (5 dias úteis = 40 story points / 2 devs)      │
│  Input: Tasks aprovadas                                         │
│  Owner: Dev Sênior + Dev Pleno (desenvolvimento paralelo)      │
│  IA tools: GitHub Copilot (código, testes), Claude (debug)     │
│  Output: Commits em feature branches, PRs abertos              │
│  ↓ GATE-4: Code Review (Tech Lead + Dev Sênior)                │
├─────────────────────────────────────────────────────────────────┤
│ REVIEW PHASE (2 dias úteis, paralelo com próximo módulo)      │
│  Input: Código mergeado em cenário-1                           │
│  Owner: QA (testa) + Tech Lead (valida)                        │
│  IA tools: Claude (análise de falhas), GitHub Copilot (tests)  │
│  Output: Test results, golden queries validadas                │
│  ↓ GATE-5: Test Review (QA + Product Specialist)               │
├─────────────────────────────────────────────────────────────────┤
│ DEPLOY PHASE (0.5 dias úteis = off-peak 22h-02h)              │
│  Input: Testes aprovados                                       │
│  Owner: Tech Lead (técnico) + Delivery Mgr (coordenação)       │
│  IA tools: Claude Cowork (automação runbook), Claude (análise) │
│  Output: Produção deployada, monitoring ativo                  │
│  ↓ GATE-6: Deploy Ready (Tech Lead + Delivery Mgr)             │
└─────────────────────────────────────────────────────────────────┘
```

---

## 3. Papéis × Ferramentas de IA por Fase

| Papel | Spec | Plan | Tasks | Implement | Review | Deploy |
|-------|------|------|-------|-----------|--------|--------|
| **Product Specialist** | Claude Design + Claude (req) | Claude (refinement) | — | — | Claude (validação) | — |
| **Tech Lead** | Claude (validação) | Claude (arquitetura, risco) | GitHub Copilot (exemplos) | GitHub Copilot (review) | Claude (padrões) | Claude Cowork (runbook) |
| **Dev Sênior** | Discussão | Claude (pair review) | GitHub Copilot (decomp) | GitHub Copilot (código) | Claude (debug) | — |
| **Dev Pleno** | — | Estuda | GitHub Copilot (est) | GitHub Copilot (código) | GitHub Copilot (testes) | — |
| **QA** | Claude (cenários) | Claude (plano testes) | Claude (casos teste) | Acompanha | Claude (falhas) + GitHub Copilot (tests) | Claude (staging) |
| **Delivery Manager** | Claude (timeline) | Claude (risk) | Claude (velocidade) | Claude Cowork (status) | Claude Cowork (gates) | Claude Cowork (coord) |

---

## 4. Ciclo de Planejamento (Sprints de 2 semanas)

Cada sprint cobre **1 módulo** (pipeline-ingestao, query-endpoint, feedback-api, teams-bot, painel-web).

### Sprint Schedule (exemplo Sprint 1, Jun 19-30)

```
SEMANA 1: Jun 19-23 (Seg-Sex)
  Seg 19:   Spec inicia (GATE-1 até ter 20)
  Ter 20:   Plan inicia (GATE-2 até qua 21)
  Qua 21:   Tasks aprovadas (GATE-3 até qua 21)
  Qua 21:   Implement inicia (Dev começa code)
  Qui 22:   Implement continua
  Sex 23:   Implement continua

SEMANA 2: Jun 26-30 (Seg-Fri)
  Seg 26:   Code Review inicia (PRs abrem, GATE-4 até ter 27)
  Ter 27:   Review QA inicia (testes, GATE-5 até qua 28)
  Qua 28:   Review QA termina (todas golden queries validadas)
  Qui 29:   Deploy window (off-peak 22h-02h, GATE-6 aprovado)
  Sex 30:   Monitoring ativo, no issues

Paralelo (Seg 26 onwards):
  Sprint +1 Module 2: Spec inicia
  (não bloqueia Sprint 1, trabalho em paralelo com 2 devs)
```

### Velocidade Esperada

- **1 sprint = 1 módulo = ~40 story points**
- **5 módulos = 5 sprints = ~10 semanas (2.5 meses)**
- **Buffer: +1-2 semanas para testes de integração, deploy, operacionalização**
- **Timeline realista: jun 23 - set 15 (fase inicial), set 15 - out 15 (hardening, ops)**

---

## 5. Validation Gates — Sumário Executivo

| Gate | Fase | Owner | O quê? | Timebox | Se falhar |
|------|------|-------|--------|---------|-----------|
| **GATE-1** | Spec → Plan | Tech Lead | Chunks ref? SLAs válidos? AC testáveis? | 24h | Product Spec volta |
| **GATE-2** | Plan → Tasks | Tech Lead + Delivery Mgr | Arquitetura? Risco? Alocação ok? | 24h | Simplifica scope |
| **GATE-3** | Tasks → Implement | Tech Lead | Tasks < 13pt? AC não vago? Skill mapeada? | 12h | Dev Sênior ajusta |
| **GATE-4** | Code → Merge | Tech Lead + Dev Sênior | CI verde? Skill pattern? Sem console.log? Edge cases? | 4h | Dev faz commit fix |
| **GATE-5** | Tests → Deploy | QA + Product Specialist | Coverage > 80%? Golden queries + fonte? | 48h | Retorna antes deploy |
| **GATE-6** | Staging → Prod | Tech Lead + Delivery Mgr | Infra ok? Runbook testado? Monitoring ativo? | 4h | Rollback < 30min |

**Template completo:** `/docs/gates/validation-gates-template.md`

---

## 6. Comunicação & Alinhamento

### Ritmo Semanal

| Dia | Reunião | Duração | Owner | Agenda |
|-----|---------|---------|-------|--------|
| **Seg** | Weekly Planning | 30min | Tech Lead + Delivery Mgr | Sprint plan, alocação, blockers |
| **Qua** | Checkpoint | 15min | Delivery Mgr | Status GATE, velocidade, risco |
| **Sex** | Retrospective | 30min | Time (all) | O que deu certo, o que não deu, ajustes |

### Status Report (Diário)

**Delivery Manager** usa Claude Cowork para gerar daily status:
```
Entrada: Azure DevOps board (work items, PRs, test results)
Saída: Slack message no #novatech-status
Formato:
  ✓ Tasks completed: NOVA-X.1, NOVA-X.2
  ⏳ In progress: NOVA-X.3 (Dev Sênior, 80% done)
  ⚠️ Blockers: AI Search indexing slow (escalado para CTO)
  📊 Velocity: 28/40 points (70%, on track)
  🚦 Gates: GATE-1 approved, GATE-2 in review (Tech Lead)
```

---

## 7. Integrações com Ferramentas

### GitHub + Azure DevOps

- **GitHub:** Feature branches, PRs, CI/CD, code history
- **Azure DevOps:** Work items, sprints, boards, tracking
- **Link:** Cada PR linkado a work item (NOVA-X.Y), cada work item tem gate checklist attachment

### Sistema de Artefatos

```
Repository: db1/novatech-assistant
├── /specs/{modulo}/
│   ├── requirements.md (GATE-1)
│   ├── plan.md (GATE-2)
│   └── tasks.md (GATE-3)
├── /skills/
│   ├── foundation/ (padrões base)
│   ├── domain/ (Azure, React, TypeScript)
│   └── artifact/ (how-tos para cada tipo de tarefa)
├── /prompts/
│   ├── system-prompt.md (versionado, changelog)
│   └── eval/ (golden-queries.json, eval-results/)
├── /docs/
│   ├── gates/ (GATE checklists preenchidos)
│   ├── runbooks/ (deploy, troubleshooting)
│   └── adr/ (Architecture Decision Records)
└── /src/
    ├── functions/ (Azure Functions)
    ├── services/ (integração RAG, OpenAI)
    ├── bot/ (Teams bot)
    └── tests/ (unit, integration, e2e)
```

---

## 8. Gestão de Risco & Escalação

### Matriz de Risco

| Risco | Prob | Impacto | Mitigação | Dono |
|-------|------|---------|-----------|------|
| Alucinação em RAG (resposta factualmente errada) | Alta | Crítico | GATE-5: golden queries + fonte verificável | QA |
| Contradição PROC-042 v1 vs v2 | Alta | Alto | GATE-1/2: metadata vigência, teste regressão | Tech Lead |
| Cargas perigosas: resposta permite devolução | Alta | Crítico | GATE-1: POL-001-B referenciado, teste de rejeição | Product Spec |
| Latência creep (individual ok, soma quebra SLA) | Média | Alto | GATE-2: latência acumulada estimada | Tech Lead |
| Dev Pleno pula code review (confiança em Copilot) | Média | Alto | GATE-4: timebox rigoroso 4h, Tech Lead assina | Tech Lead |
| Spec fica parada 3 semanas | Baixa | Médio | SLA 24h com escalação CTO automática | Delivery Mgr |

### Escalation Path

```
GATE-1 falha > 24h
  → Escalação: CTO review, força decisão (aprova, simplifica, ou bloqueia)

GATE-2 falha > 24h
  → Escalação: Tech Lead + CTO redimensionam (simplifica scope ou estende prazo)

GATE-3 falha > 12h
  → Escalação: Tech Lead força aprovação (pode aceitar risk baixo)

GATE-4 (code review) leva > 4h
  → Escalação: Automática na 2h mark (Dev Sênior + Tech Lead pair review)

GATE-5 (QA testes) leva > 48h
  → Escalação: Product Lead + Tech Lead decidem se postpone deploy ou força merge com known issues

GATE-6 (deploy) falha
  → Rollback automático < 30min, post-mortem 2h depois

CTO não responde em 24h (raro)
  → Delivery Manager decide unilateralmente com Tech Lead, documenta desvio
```

---

## 9. Critérios de Sucesso (Por Sprint)

Um sprint é considerado **SUCESSO** se:

- ✓ Todas as 6 GATES passaram (nenhuma reprova)
- ✓ Velocity: 35-40 story points (≥85% do planejado)
- ✓ Code coverage: ≥80% para novo código
- ✓ Bugs críticos em produção: 0
- ✓ SLA de latência (P95 < 2s): mantido
- ✓ Testes de regressão: 100% passando
- ✓ Golden queries de RAG: 100% com fonte verificável

Um sprint é **PARCIALMENTE SUCESSO** (aceito, com retro) se:

- ⚠️ 1 reprova em gate (foi corrigido na mesma sprint)
- ⚠️ Velocity 30-35 (70-85%)
- ⚠️ 1 bug crítico encontrado e fixado em produção
- ⚠️ Latência P95 degradou 20-30% (abaixo de SLA, mas aceitável com plano de otimização)

Um sprint é **FAILED** (replan necessário) se:

- ✗ >1 reprova em gate (não corrigido na sprint)
- ✗ Velocity <30 (< 70%)
- ✗ >1 bug crítico simultâneo em produção
- ✗ Latência P95 >3s (viola SLA NovaTech)
- ✗ Golden queries com respostas alucinadas (não detectadas até deploy)

---

## 10. Métricas & Observabilidade

### Dashboard de Delivery Manager (atualizado diariamente via Claude Cowork)

```
SPRINT METRICS
  Velocity: 28/40 points (70%, on track)
  Sprint burndown: [━━━━┃━━━━━] 3 dias restantes
  
GATE METRICS
  GATE-1: 1/1 passed (0 failed)
  GATE-2: 1/1 passed (0 failed)
  GATE-3: 1/1 passed (0 failed)
  GATE-4: 0/2 in progress (2 pending review)
  GATE-5: pending
  GATE-6: pending
  
CODE METRICS
  Commits: 14 (avg 2 per day)
  PRs: 3 (1 merged, 2 in review)
  CI success rate: 100%
  Test coverage: 84% (target: 80%)
  
QUALITY METRICS
  Golden queries: 5/5 passed (100%)
  Golden queries with source: 5/5 (100%)
  Critical bugs: 0
  High severity bugs: 1 (known issue, low risk)
  
TEAM METRICS
  Dev Sênior: 12 points done, 8 in progress (on pace)
  Dev Pleno: 10 points done, 10 in progress (slightly behind)
  QA: test coverage at 84%, golden queries validated
  Tech Lead: 12 PRs reviewed, avg review time 2.5h
  
RISK METRICS
  Latency P95: 1.8s (baseline 1.6s, +12% acceptable)
  Token usage: 64% of quota (safe)
  Replan needed? NO
```

### KPIs por Sprint (dados históricos)

```
Sprint | Velocity | Coverage | Gate Pass | Bugs | Latency P95 | Status
     1 | 40/40    | 84%      | 6/6      | 0    | 1.8s        | ✓ Success
     2 | 38/40    | 86%      | 6/6      | 0    | 1.9s        | ✓ Success
     3 | 36/40    | 82%      | 5/6*     | 1    | 2.1s        | ⚠️ Partial (1 reprova, fixado)
     4 | 35/40    | 81%      | 6/6      | 0    | 1.7s        | ✓ Success
     5 | 32/40    | 79%      | 4/6**    | 2    | 2.5s        | ✗ Failed (replan)

* GATE-3 reprova: tasks estimadas errado, corrigidas em 6h
** Sprint 5: GATE-2 e GATE-4 com múltiplas reprovações, scope reduzido, estendido
```

---

## 11. Checklist Pré-Go-Live

**Antes de começar Sprint 1 (sexta 23/06):**

```
☐ Infraestrutura
  ☐ Azure resources provisionados (AI Search, OpenAI, Functions, Cosmos)
  ☐ CI/CD pipeline funcionando (GitHub Actions: lint, test, build)
  ☐ Secrets em Key Vault (nenhuma credencial em código)

☐ Documentação
  ☐ ADRs finalizados (0001-0004)
  ☐ Repositório estruturado (skills, specs, prompts, docs)
  ☐ AGENTS.md escrito (constitution do projeto)
  ☐ Chunks de referência (Anexo B) disponíveis para QA

☐ Acesso
  ☐ Time tem acesso ao repositório (GitHub)
  ☐ Dev tem GitHub Copilot ativo
  ☐ Todos têm acesso a Claude
  ☐ Product Specialist tem Claude Design
  ☐ Delivery Manager tem Claude Cowork

☐ Processo
  ☐ Validation gates template copiado para /docs/gates/
  ☐ Reunião de alinhamento executada (30min, todas papéis)
  ☐ Azure DevOps board configurado (fields: Module, Task, Gate, Status)
  ☐ Daily standup scheduled (15min, 09h30 brasília)
  ☐ Weekly planning scheduled (30min segunda, 10h)
  ☐ Escalation contacts definidos e comunicados

☐ Time
  ☐ Onboarding concluído (tech stack, padrões, tools)
  ☐ Tech Lead faz pair programming de exemplo (primeira task)
  ☐ QA entende golden queries (Anexo B) e teste de fonte verificável
  ☐ Product Specialist leu todos os documentos do cliente (POL, PROC, SLA, chunks)

Status: ☐ READY / ☐ BLOQUEADO (descrever abaixo)
```

---

## 12. Contatos & Responsabilidades Finais

| Papel | Pessoa | Telefone | Slack | Responsabilidades |
|-------|--------|----------|-------|-------------------|
| **Delivery Manager** | Jacque | — | @jacque | Orquestra gates, status reporting, risk log |
| **Tech Lead** | (nome) | — | @tech-lead | GATE-1, 2, 3, 4, 6 aprovador, escalação |
| **Product Specialist** | (nome) | — | @product | GATE-1 writer, GATE-5 validador |
| **QA Lead** | (nome) | — | @qa | GATE-5 aprovador, golden queries, teste fonte |
| **Dev Sênior** | (nome) | — | @dev-sênior | GATE-3 decompõe, GATE-4 code review |
| **Dev Pleno** | (nome) | — | @dev-pleno | Implement, GATE-4 PR autor |
| **CTO** | (nome) | — | @cto | Escalação final (raro), decisões arquiteturais |

---

## 13. Próximos Passos

1. **Hoje (18/06):** Jacque aprova documento
2. **Amanhã (19/06):** Reunião de alinhamento (30min, todas papéis)
3. **Quinta (20/06):** Tech Lead faz pair programming de exemplo (task NOVA-0.1)
4. **Sexta (23/06):** Go-live Sprint 1 — Spec phase inicia
5. **26/06:** Primeira review de processo (retrospective)

---

## 14. Apêndice: Integração com Cowork

Claude Cowork (automação para Delivery Manager) executa diariamente:

```
Entrada: Azure DevOps API + GitHub API
Tarefas:
  1. Pull dados de work items (status, pontos, datas)
  2. Pull dados de PRs (review time, approvals)
  3. Pull dados de test results (coverage, failures)
  4. Calcular velocity, burndown, gate status
  5. Gerar daily summary em Slack
  6. Alertar se SLA violado (gate > timebox)
  7. Sugerir ações (ex: "Tech Lead, GATE-1 expira em 4h")

Saída: Slack → #novatech-status (diário 09h)
       Email → delivery-manager@db1.com (diário 09h30)
       Dashboard → internal wiki (atualizado em tempo real)
```

Cowork **não toma decisões**, apenas automatiza coleta de dados + alertas.

---

**Fim do documento. Versão 2.0 pronta para operação.**

Data de preparação: 18/06/2026  
Preparado por: CTO (com input de Jacque Delivery Manager)  
Última atualização: 18/06/2026  
Próxima revisão: 30/07/2026 (após sprint 2)
