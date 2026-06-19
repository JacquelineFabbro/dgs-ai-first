# Specs Tracking Board — NovaTech Assistant

**Data:** 18/06/2026  
**Sprint:** Sprint 1 (19/06 - 30/06)  
**Owner:** Delivery Manager (Jacque)  
**Última atualização:** 18/06/2026 09:00 BRT

---

## 📊 Dashboard Executivo

```
OVERVIEW — Todos os Módulos

Rascunho        Em Revisão      Aprovada        Em Implementação    Validada
   0 specs         0 specs         0 specs              0 specs          0 specs
  ────────────────────────────────────────────────────────────────────────
   [ ]             [ ]             [ ]                  [ ]              [ ]
```

**Status Geral:** 🔵 PRONTO PARA INICIAR (0/5 modules started)

---

## 🎯 Kanban Visual (Formato Tabular)

| # | Módulo | requirements.md | plan.md | tasks.md | Status Geral | Owner | ETA |
|---|--------|-----------------|---------|----------|--------------|-------|-----|
| 1 | **pipeline-ingestao** | 🔴 Rascunho | 🔴 Pendente | 🔴 Pendente | PARADO | Product Spec | Jun 23 |
| 2 | **query-endpoint** | 🔴 Rascunho | 🔴 Pendente | 🔴 Pendente | PARADO | Product Spec | Jun 26 |
| 3 | **feedback-api** | 🔴 Rascunho | 🔴 Pendente | 🔴 Pendente | PARADO | Product Spec | Jul 7 |
| 4 | **teams-bot** | 🔴 Rascunho | 🔴 Pendente | 🔴 Pendente | PARADO | Product Spec | Jul 18 |
| 5 | **painel-web** | 🔴 Rascunho | 🔴 Pendente | 🔴 Pendente | PARADO | Product Spec | Jul 29 |

---

## 📋 Board Detalhado por Estado

### 1️⃣ RASCUNHO (Product Specialist escrevendo)

```
┌─────────────────────────────────────────────────────────────┐
│ requirements.md Sendo Escrito                               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 🔴 pipeline-ingestao/requirements.md                        │
│    Owner: Product Specialist                               │
│    Status: Escrevendo (não iniciado)                        │
│    ETA: 19/06 09h                                           │
│    Progresso: [ ] 0%                                        │
│                                                             │
│ 🔴 query-endpoint/requirements.md                           │
│    Owner: Product Specialist                               │
│    Status: Aguardando Sprint 2                             │
│    ETA: 26/06 09h                                           │
│    Progresso: [ ] 0%                                        │
│                                                             │
│ 🔴 feedback-api/requirements.md                             │
│    Owner: Product Specialist                               │
│    Status: Aguardando Sprint 3                             │
│    ETA: 07/07 09h                                           │
│    Progresso: [ ] 0%                                        │
│                                                             │
│ 🔴 teams-bot/requirements.md                                │
│    Owner: Product Specialist                               │
│    Status: Aguardando Sprint 4                             │
│    ETA: 18/07 09h                                           │
│    Progresso: [ ] 0%                                        │
│                                                             │
│ 🔴 painel-web/requirements.md                               │
│    Owner: Product Specialist                               │
│    Status: Aguardando Sprint 5                             │
│    ETA: 29/07 09h                                           │
│    Progresso: [ ] 0%                                        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 2️⃣ EM REVISÃO (Tech Lead validando com GATE)

```
┌─────────────────────────────────────────────────────────────┐
│ Aguardando Validação / Feedback                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ [Nenhuma spec em revisão no momento]                        │
│                                                             │
│ Próximas esperadas:                                         │
│   • pipeline-ingestao/requirements.md → GATE-1              │
│     ETA: 19/06 até 20/06 17h (24h SLA)                     │
│                                                             │
│   • pipeline-ingestao/plan.md → GATE-2                      │
│     ETA: 20/06 até 21/06 17h (24h SLA)                     │
│                                                             │
│   • pipeline-ingestao/tasks.md → GATE-3                     │
│     ETA: 21/06 até 21/06 17h (12h SLA)                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 3️⃣ APROVADA (Pronta para implementação)

```
┌─────────────────────────────────────────────────────────────┐
│ Validadas pelos Gates — Prontas para Próxima Fase           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ [Nenhuma spec aprovada no momento]                          │
│                                                             │
│ Esperadas após GATE:                                        │
│   • pipeline-ingestao/requirements.md                       │
│     GATE-1 approval: esperado 20/06 17h                    │
│     Próximo: Tech Lead começa plan.md                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 4️⃣ EM IMPLEMENTAÇÃO (Dev codando baseado em spec)

```
┌─────────────────────────────────────────────────────────────┐
│ Specs Sendo Usadas para Development                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ [Nenhuma spec em implementação no momento]                  │
│                                                             │
│ Esperadas:                                                  │
│   • pipeline-ingestao/tasks.md                              │
│     Início estimado: 21/06 (após GATE-3)                   │
│     Dev: Dev Sênior                                         │
│     Tasks: NOVA-1.1 até NOVA-1.7 (7 tasks)                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 5️⃣ VALIDADA (QA aprovou, pronta para deploy)

```
┌─────────────────────────────────────────────────────────────┐
│ Implementação Completa — Aprovada por QA (GATE-5)           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ [Nenhuma spec validada no momento]                          │
│                                                             │
│ Esperadas:                                                  │
│   • pipeline-ingestao (todos 3 arquivos)                    │
│     GATE-5 approval esperado: 28/06 17h                    │
│     Próximo: Deploy (GATE-6)                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 📈 Timeline Esperada por Módulo

### Módulo 1: pipeline-ingestao
```
Jun 19 ──────────────────────────────────────────────── Jun 30
  │         │         │         │         │         │
  ▼         ▼         ▼         ▼         ▼         ▼
 REQ      GATE-1    PLAN      GATE-2   TASKS    GATE-3   IMPL    GATE-4   GATE-5   GATE-6
 │         │         │         │         │         │       │       │        │        │
19/09h   20/17h    21/09h    21/17h    21/17h    21/17h  21-26   26-27    28       29/22h
DRAFT  APPROVED  REVIEW    APPROVED  REVIEW   APPROVED  IN PROGRESS                VALIDATED
```

### Módulo 2: query-endpoint (paralelo ao final de Sprint 1)
```
Jun 26 ──────────────────────────────────────────────── Jul 7
 Similar timeline, offset by 1 week
```

### Módulo 3-5: feedback-api, teams-bot, painel-web
```
Sprints 3, 4, 5 — mesma cadência
```

---

## 🔄 Fluxo de Mudança de Estado

```
RASCUNHO
  │
  ├─→ [Product Specialist escreve requirements.md]
  │
  └──→ EM REVISÃO (GATE-1)
        │
        ├─→ [Tech Lead valida checklist]
        │
        └──→ APROVADA ou RASCUNHO (se REQUEST CHANGES)
              │
              ├─→ [Tech Lead escreve plan.md]
              │
              └──→ EM REVISÃO (GATE-2)
                    │
                    ├─→ [Tech Lead + Delivery Mgr validam]
                    │
                    └──→ APROVADA ou EM REVISÃO (se REQUEST CHANGES)
                          │
                          ├─→ [Dev Sênior gera tasks.md]
                          │
                          └──→ EM REVISÃO (GATE-3)
                                │
                                ├─→ [Tech Lead valida]
                                │
                                └──→ APROVADA
                                      │
                                      ├─→ [Dev implementa (NOVA-1.1 até 1.7)]
                                      │
                                      ├─→ EM IMPLEMENTAÇÃO
                                      │   ├─→ GATE-4: Code Review
                                      │   ├─→ GATE-5: Test Review
                                      │   │
                                      │
                                      └──→ VALIDADA (GATE-6: Deploy)
```

---

## 📊 Tabela de Rastreamento Detalhada

### Sprint 1 (19/06 - 30/06): pipeline-ingestao

| Data | Estado | Artefato | Owner | Gate | SLA | Status | Notas |
|------|--------|----------|-------|------|-----|--------|-------|
| 19/06 09h | Rascunho | requirements.md | Product Spec | — | — | 🔴 Não iniciado | Aguardando Product Specialist |
| 19/06-20/06 | Em Revisão | requirements.md | Tech Lead | GATE-1 | 24h | ⏳ Pendente | SLA até 20/06 17h |
| 20/06 17h | Aprovada | requirements.md v1.0 | — | ✅ GATE-1 | — | 🟢 OK | Tech Lead assinou |
| 20/06 17h | Rascunho | plan.md | Tech Lead | — | — | 🔴 Não iniciado | Tech Lead começa |
| 20/06-21/06 | Em Revisão | plan.md | Tech Lead + DM | GATE-2 | 24h | ⏳ Pendente | SLA até 21/06 17h |
| 21/06 17h | Aprovada | plan.md v1.0 | — | ✅ GATE-2 | — | 🟢 OK | Tech Lead + DM assinaram |
| 21/06 17h | Rascunho | tasks.md | Dev Sênior | — | — | 🔴 Não iniciado | Dev Sênior + Copilot gera |
| 21/06 17h-17h | Em Revisão | tasks.md | Tech Lead | GATE-3 | 12h | ⏳ Pendente | SLA até 21/06 17h (mesmo dia!) |
| 21/06 17h | Aprovada | tasks.md v1.0 | — | ✅ GATE-3 | — | 🟢 OK | Tech Lead assinou, IMPL começa |
| 21/06-26/06 | Em Implementação | NOVA-1.1 até 1.7 | Dev Sênior | GATE-4/5 | 5 dias | 🟡 Em progresso | Dev coding, PRs abrem |
| 26/06-28/06 | Em Implementação | Code Review | Tech Lead | GATE-4 | 4h/PR | 🟡 Em progresso | PRs em review, merge esperado |
| 26/06-28/06 | Em Implementação | Test Review | QA | GATE-5 | 48h | 🟡 Em progresso | Golden queries validadas |
| 28/06 17h | Validada | Todos specs + código + testes | — | ✅ GATE-5 | — | 🟢 OK | Pronto para deploy |
| 29/06 22h | Validada | Deploy em Produção | Tech Lead | GATE-6 | 4h | ⏳ Agendado | Off-peak deploy |
| 30/06 08h | Validada | Monitoring OK | Delivery Mgr | ✅ GATE-6 | — | 🟢 OK | Sprint 1 completo |

---

## 🎯 Legenda de Status

### Estados Principais

| Estado | Emoji | Descrição | Owner |
|--------|-------|-----------|-------|
| **Rascunho** | 🔴 | Sendo escrito, não pronto para revisão | Product Spec / Tech Lead / Dev |
| **Em Revisão** | 🟡 | Esperando aprovação em GATE | Tech Lead / QA |
| **Aprovada** | 🟢 | Passou em GATE, pronta para próxima fase | — |
| **Em Implementação** | 🔵 | Sendo usada para desenvolvimento | Dev / QA |
| **Validada** | ✅ | Completa, QA aprovou, pronto para deploy | — |

### Ícones Adicionais

| Ícone | Significado |
|-------|------------|
| ⏳ | Aguardando ação (SLA rodando) |
| ✅ | Gate aprovado / completo |
| 🚫 | Bloqueado ou REQUEST CHANGES |
| ⚠️ | SLA em risco (< 2h) |
| 📌 | Precisa de atenção imediata |

---

## 📱 Como Usar Este Board

### Para Delivery Manager (Atualizar Diariamente)

```
1. Abrir este arquivo todos os dias 09h
2. Verificar: qual spec mudou de estado?
3. Atualizar tabelas e progresso
4. Se SLA em risco (< 2h): marca ⚠️ e alerta no Slack
5. Daily report via Cowork: "X specs em revisão, Y aprovadas"
```

### Para Qualquer Membro do Time (Consultar)

```
1. Abrir este arquivo anytime
2. Ver estado atual de cada spec
3. Ver quando spec é esperada chegar em "Aprovada"
4. Ver próximos passos (qual owner está esperado fazer o quê)
5. Verificar SLA de cada GATE
```

### Para Tech Lead (Validação)

```
1. Diariamente às 09h: verificar "Em Revisão"
2. Se specs estão esperando GATE: começar validação
3. Após validação: mover para "Aprovada" + assinar
4. Comentário: "GATE-X approved by Tech Lead, yyyy-mm-dd hh:mm"
```

### Para Product Specialist (Escrita)

```
1. Quando time está pronto para Sprint N
2. Escrever requirements.md para módulo N
3. Submeter para GATE-1 (Tech Lead review)
4. Se REQUEST CHANGES: corrigir e resubmeter
5. Se APPROVED: Tech Lead começa plan.md
```

---

## 📊 Progresso Geral da Sprint

### Sprint 1 (19/06 - 30/06) - pipeline-ingestao

```
Semana 1: Jun 19-23 (Spec Phases)
├─ Jun 19: requirements.md fase (GATE-1)
├─ Jun 20: plan.md fase (GATE-2)
├─ Jun 21: tasks.md fase (GATE-3)
└─ Jun 21: Implementation inicia

Semana 2: Jun 26-30 (Implementation + Review + Deploy)
├─ Jun 26: Code Review inicia (GATE-4)
├─ Jun 26: Test Review inicia (GATE-5)
├─ Jun 29: Deploy window (GATE-6, off-peak)
└─ Jun 30: Monitoring OK, Sprint 1 completo

Timeline: ████████░░░░░░░░░░░░░░░░░ (30% done by Jun 23)
```

### Sprint 2 (26/06 - 07/07) - query-endpoint (paralelo ao final Sprint 1)

```
Semana 1: Jun 26-30 (Spec Phases)
├─ Jun 26: requirements.md fase (GATE-1)
├─ Jun 27: plan.md fase (GATE-2)
├─ Jun 28: tasks.md fase (GATE-3)
└─ Jun 28: Implementation inicia

Timeline: ░░░░░░░░░░░░░░░░░░░░░░░░░░ (0% — aguardando)
```

---

## 🔔 Alertas & SLA Tracking

### Gates com SLA

| Gate | SLA | Escalação | Responsável |
|------|-----|-----------|------------|
| GATE-1 (Spec) | 24h | CTO auto-escalates | Tech Lead |
| GATE-2 (Plan) | 24h | CTO auto-escalates | Tech Lead + DM |
| GATE-3 (Tasks) | 12h | Tech Lead simplifica | Tech Lead |
| GATE-4 (Code) | 4h/PR | Auto retry + Slack | Tech Lead |
| GATE-5 (Tests) | 48h | Paralelo com próximo | QA |
| GATE-6 (Deploy) | 4h | On-call escalates | Tech Lead + DM |

### Próximos Alertas Esperados

```
Jun 19 09h: requirements.md submission expected
Jun 19 17h: Reminder (if not submitted by 17h)
Jun 20 09h: Tech Lead GATE-1 review begins
Jun 20 17h: GATE-1 SLA expires (approval or escalation)
Jun 21 09h: Tech Lead GATE-2 review begins
Jun 21 17h: GATE-2 SLA expires (approval or escalation)
Jun 21 17h: Dev Sênior GATE-3 review begins (same day!)
Jun 21 17h: GATE-3 SLA expires (tight!)
Jun 26 09h: GATE-4 (Code Review) expected
Jun 28 17h: GATE-5 (Test Review) deadline
Jun 29 22h: GATE-6 (Deploy) window
```

---

## 📝 Notas & Observações

```
Jun 18, 18:00:
  - Board criado com 5 módulos como itens iniciais
  - Timeline esperada: Sprint 1 (pipeline-ingestao) Jun 19-30
  - Sprints 2-5 cada uma com 1 módulo
  - Total projeto: ~10 semanas (5 sprints × 2 semanas)

Jun 19 (esperado):
  - Product Specialist submete pipeline-ingestao/requirements.md
  - GATE-1 review inicia
  - Board será atualizado com status real

Jun 20 (esperado):
  - GATE-1 resultado (aprovado ou reject)
  - Se aprovado: plan.md escrita inicia

Jun 21 (esperado):
  - GATE-2 resultado
  - GATE-3 (tasks) mesmo dia (tight SLA)
  - Dev começa implementation

Jun 26-29:
  - Code review (GATE-4)
  - Test review (GATE-5)
  - Deploy (GATE-6, off-peak)

Jun 30:
  - Sprint 1 wrap-up
  - Monitoring report
  - Retrospectiva
  - Sprint 2 planning
```

---

## 🔗 Integração com Outras Ferramentas

### Azure DevOps Link

Cada estado do board corresponde a **work item state**:

```
Rascunho            → Work Item State: "New"
Em Revisão          → Work Item State: "Active" + Assigned to reviewer
Aprovada            → Work Item State: "Done" + Tag: "gate-approved"
Em Implementação    → Work Item State: "Active" + Multiple child tasks
Validada            → Work Item State: "Done" + All child tasks done
```

### GitHub Link

Cada transição de estado é commitada:

```
Rascunho → Em Revisão:
  No commit (apenas local)

Em Revisão → Aprovada:
  git commit -m "approve: pipeline-ingestao/requirements — GATE-1 passed"

Em Implementação → Validada:
  Multiple PRs merged
  git commit -m "approve: pipeline-ingestao — GATE-5 passed"
```

---

## 📥 Download & Uso

Este board pode ser:

1. **Consultado aqui** (markdown, copy-paste)
2. **Importado em Excel/Sheets** (tabelas como CSV)
3. **Linkado ao Azure DevOps** (via queries)
4. **Exibido em TV** (painel físico no escritório)
5. **Compartilhado diariamente** (Cowork gera snapshot Slack)

---

## ✅ Checklist: Antes de Iniciar Sprint 1

```
☐ Board criado e compartilhado (este arquivo)
☐ Todos entendem: 5 estados, qual owner move o quê
☐ SLAs explicadas (24h GATE-1, 24h GATE-2, 12h GATE-3)
☐ Escalation path claro (quem alertar se SLA violado)
☐ Product Specialist pronto para submeter requirements.md (Jun 19 09h)
☐ Tech Lead pronto para revisar (Jun 19, até 20/06 17h)
☐ Dev Sênior pronto para gerar tasks (Jun 21, até 21/06 17h)
☐ Daily update time definido (Delivery Manager, 09h)
☐ Slack channel criado (#novatech-specs) para notificações
☐ Board impresso (opcional, para parede do escritório)
```

---

**Fim do Documento.**

Data criação: 18/06/2026  
Próxima atualização: 19/06/2026 09h (esperado: requirements.md submission)  
Owner: Delivery Manager (Jacque)

Para questões: Slack @delivery-manager ou email delivery-manager@db1.com
