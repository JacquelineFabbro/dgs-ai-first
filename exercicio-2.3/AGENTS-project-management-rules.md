# Project Management Rules

**Purpose:** Rules for AI agents (Claude, Copilot, Cowork) generating management artifacts, tasks, documentation, and status reports.

**Last Updated:** 2026-06-18  
**Owner:** Tech Lead + Delivery Manager  
**Audience:** AI agents and automation systems  
**Format:** Machine-readable specification (prescriptive)

---

## 1. Task & Issue Naming Rules

### 1.1 Task ID Format

**Rule:** All tasks MUST follow format `NOVA-{module}-{sequence}`

**Specification:**
```
Format:           NOVA-{module}-{sequence}
Module:           [1..5] (maps to module number in sequence)
Sequence:         [1..99] (sequential within module)
Example Valid:    NOVA-1.1, NOVA-1.2, NOVA-2.5, NOVA-5.12
Example Invalid:  NOVA-pipeline-ingestao-1, NOVA_1_1, NOVA1.1, nova-1.1
```

**Module Mapping:**
```
NOVA-1: pipeline-ingestao (ingest documents, chunk, embed, index)
NOVA-2: query-endpoint (search with RAG, return answer + sources)
NOVA-3: feedback-api (log incorrect responses, track failures)
NOVA-4: teams-bot (conversational interface in Teams)
NOVA-5: painel-web (dashboard, metrics, chat history)
```

### 1.2 Task Title Format

**Rule:** Task titles MUST be concise, action-oriented, and in English

**Specification:**
```
Format:         [Verb] [Object] [Qualifier]
Max length:     50 characters
Language:       English only
Tense:          Imperative (infinitive without "to")
Capitalization: Title Case

Example Valid:
  "Create PDF extraction handler"
  "Implement 20% overlap chunking"
  "Validate PROC-042 version handling"
  "Add date filtering to query response"

Example Invalid:
  "PDF Extraction Handler Creation Process" (too long, not imperative)
  "Extrair PDFs" (Portuguese, should be English)
  "fixing bugs in code" (lowercase, not action-oriented)
```

### 1.3 Issue/PR Title Format

**Rule:** GitHub issues and PRs MUST follow conventional commits format

**Specification:**
```
Format:         {type}({scope}): {description}
Type:           [feat|fix|docs|refactor|test|chore]
Scope:          [module-slug] (e.g., pipeline-ingestao, query-endpoint)
Description:    Concise, lowercase, < 72 chars total
No period:      Title should NOT end with period

Example Valid:
  "feat(pipeline-ingestao): implement chunking with overlap"
  "fix(query-endpoint): handle empty search results"
  "docs(feedback-api): add error handling documentation"
  "test(teams-bot): add conversation flow tests"
  "refactor(painel-web): extract metrics component"

Example Invalid:
  "feat(pipeline-ingestao): implementing chunking" (gerund, not desc)
  "feat: implement chunking" (missing scope)
  "Feature: Implement chunking" (wrong format)
```

### 1.4 Labels (Azure DevOps Tags)

**Rule:** Each work item MUST have ALL of these labels

**Specification:**
```
Mandatory labels (all required):
  - Module: [pipeline-ingestao | query-endpoint | feedback-api | teams-bot | painel-web]
  - Gate: [GATE-1 | GATE-2 | GATE-3 | GATE-4 | GATE-5 | GATE-6]
  - Status: [Blocked | Active | Review | Done]
  - Type: [Spec | Task | Bug | Improvement | Documentation]
  - Priority: [Critical | High | Medium | Low]

Optional labels (if applicable):
  - Blocker (if blocking other work)
  - Client-Request (if from client)
  - Technical-Debt (if addressing technical debt)
  - Documentation (if purely docs)

Example label set for NOVA-1.2:
  Labels: ["pipeline-ingestao", "GATE-4", "Active", "Task", "High"]
```

---

## 2. Documentation of Decisions (ADR)

### 2.1 What Requires an ADR

**Rule:** Every technical decision or scope decision MUST be documented as ADR

**Decisions that REQUIRE ADR:**
```
Technical Decisions:
  ✓ Stack choice (e.g., "Azure AI Search over Pinecone")
  ✓ Architecture pattern (e.g., "RAG with system prompts")
  ✓ Dependency selection (e.g., "pdfplumber over PyPDF2")
  ✓ Performance tradeoff (e.g., "cache over speed optimization")
  ✓ Deprecated API/library replacement (e.g., "ada-002 to text-embedding-3-small")

Scope Decisions:
  ✓ Feature exclusions (e.g., "OCR not supported in v1")
  ✓ Constraint definitions (e.g., "max chunk size = 1500 tokens")
  ✓ SLA commitments (e.g., "P95 latency < 2s")
  ✓ Risk mitigations (e.g., "version handling for PROC-042 v1 vs v2")

Decisions that DO NOT require ADR:
  ✗ Code refactoring without architecture impact
  ✗ Bug fixes (document in commit message, not ADR)
  ✗ Minor UI improvements
  ✗ Local variable naming
```

### 2.2 ADR File Location & Naming

**Rule:** All ADRs MUST be in `/docs/adr/` with specific naming

**Specification:**
```
Location:       /docs/adr/{NNNN}-{slug}.md
NNNN:           Zero-padded sequence (0001, 0002, 0003, ...)
slug:           Kebab-case, < 50 chars, descriptive
Language:       English only

Example paths:
  /docs/adr/0001-azure-ai-search-for-rag.md
  /docs/adr/0002-exclude-ocr-from-scope.md
  /docs/adr/0003-proc-042-version-handling-metadata.md
  /docs/adr/0004-text-embedding-3-small-model-selection.md

Invalid paths:
  /docs/ADR/0001-...md (wrong directory capitalization)
  /docs/adr/001-...md (wrong padding, should be 0001)
  /docs/adr/azure-ai-search.md (missing sequence number)
```

### 2.3 ADR Template (Machine-Readable Format)

**Rule:** All ADRs MUST follow this exact template structure

**Specification:**
```markdown
# ADR-{NNNN}: {Title}

**Status:** [Proposed | Accepted | Deprecated | Superseded by ADR-XXXX]  
**Date:** {YYYY-MM-DD}  
**Decider(s):** {Role(s) who decided: Tech Lead, Product Lead, CTO}  
**Consensus:** [Yes | Disagreement noted]  

## Context

{Why this decision was needed? What problem does it solve?}
{Reference to requirements, risks, or constraints.}

## Decision

{What decision was made? Be specific and prescriptive.}
{Reference NovaTech-specific context: modules, modules, gates, rules.}

## Consequences

### Positive
- {Benefit 1}
- {Benefit 2}

### Negative
- {Drawback 1}
- {Drawback 2}

### Mitigation (if applicable)
- {How negative consequence is handled}

## Alternatives Considered

### Alternative A: {Description}
- Pros: {advantages}
- Cons: {disadvantages}
- **Rejected because:** {reason}

### Alternative B: {Description}
- Pros: {advantages}
- Cons: {disadvantages}
- **Rejected because:** {reason}

## Related Documents
- [Link to requirement](specs/module/requirements.md)
- [Link to plan](specs/module/plan.md)
- [Link to validation gate checklist](docs/gates/GATE-X-template.md)
- [Link to previous ADR if supersedes](docs/adr/NNNN-xyz.md)

## Implementation Notes

{If applicable: how is this decision enforced in code? Testing? Documentation?}
{Example: "Stack choice enforced via /skills/domain/azure-ai-search-endpoint.md"}

---

**Metadata for parsing:**
```
DECISION_TYPE: [Technical | Scope]
MODULE_IMPACT: [pipeline-ingestao | query-endpoint | feedback-api | teams-bot | painel-web | Multiple]
GATE_RELEVANT: [GATE-1 | GATE-2 | GATE-3 | GATE-4 | GATE-5 | GATE-6]
DOCUMENT_DATE: {YYYY-MM-DD}
```
```

### 2.4 When to Update ADR

**Rule:** Decisions can be updated if circumstances change, but history must be maintained

**Specification:**
```
Status transitions allowed:
  Proposed → Accepted (after consensus reached)
  Accepted → Deprecated (if no longer relevant)
  Accepted → Superseded by ADR-XXXX (if new ADR replaces this)

When updating:
  ✓ Do NOT delete old content
  ✓ Do ADD "Updated {date}: {what changed}" at top
  ✓ Do change Status field
  ✓ Do maintain git history (commit with clear message)

Example commit:
  git commit -m "docs: update ADR-0001, Azure AI Search latency optimization

  Issue: Production monitoring shows P95 latency 2.5s (SLA: < 2s)
  Change: Added caching layer recommendation
  Status: Accepted → Superseded by ADR-0005-embedding-caching
  Related: NOVA-1.9 (optimization task)"
```

---

## 3. Validation Gates Specification

### 3.1 Gate Definitions (Machine-Readable)

**Rule:** Agents MUST validate against these gates before advancing phases

**Specification Format:**
```yaml
Gate:
  id: "GATE-{N}"
  name: "{Gate Name}"
  phase_before: "{Current Phase}"
  phase_after: "{Next Phase}"
  owner_approver: "[Role(s) who can approve]"
  sla_hours: {Number}
  sla_escalation: "{Escalation path if SLA violated}"
  checklist_file: "docs/gates/GATE-{N}-template.md"
  input_artifact: "{File(s) to be reviewed}"
  output_decision: "[APPROVED | REQUEST_CHANGES | REJECTED]"
  
  approval_criteria:
    - "Criterion 1"
    - "Criterion 2"
    - "Criterion N"
  
  consequence_if_rejected: "{What happens if rejected}"
```

### 3.2 All 6 Gates Definition

**Specification:**

```yaml
GATE-1:
  id: "GATE-1"
  name: "Spec Approved"
  phase_before: "requirements.md"
  phase_after: "plan.md"
  owner_approver: "Tech Lead"
  sla_hours: 24
  sla_escalation: "Escalate to CTO (auto-escalation after 24h)"
  input_artifact: "specs/{module}/requirements.md"
  output_decision: "[APPROVED | REQUEST_CHANGES | REJECTED]"
  
  approval_criteria:
    - "Arquivo existe: /specs/{module}/requirements.md"
    - "Visão geral descrita (1-2 parágrafos, não vago)"
    - "3+ user stories com AC testáveis (não 'funciona bem')"
    - "SE módulo toca RAG: chunks de referência (Anexo B) listados"
    - "SE módulo toca SLAs: tabela SLA-2024 referenciada (Gold/Silver/Standard apenas)"
    - "SE módulo toca PROC-042: ambas versões (v1 + v2) documentadas"
    - "SE módulo toca cargas perigosas: POL-001-B referenciada"
    - "Sem TBD, TODO, ou ambiguidade"
    - "Referências a base documental completas"
    - "Tech Lead e Product Lead assinaram"
  
  consequence_if_rejected: "Volta para Product Specialist, corrige requirements, resubmete"

GATE-2:
  id: "GATE-2"
  name: "Plan Approved"
  phase_before: "plan.md"
  phase_after: "tasks.md"
  owner_approver: "Tech Lead + Delivery Manager"
  sla_hours: 24
  sla_escalation: "Escalate to CTO (auto-escalation after 24h)"
  input_artifact: "specs/{module}/plan.md"
  output_decision: "[APPROVED | REQUEST_CHANGES | REJECTED]"
  
  approval_criteria:
    - "Arquivo existe: /specs/{module}/plan.md"
    - "Baseado em requirements.md aprovado (GATE-1)"
    - "Stack explícita (Azure services, libraries, patterns)"
    - "Fluxo de dados descrito (visual ou ASCII)"
    - "Risco matrix com mínimo 3 riscos, cada um com: mitigação + teste"
    - "Sequência de implementation clara (dependências explícitas)"
    - "Alocação realista (Dev Sênior, Pleno, QA, Tech Lead horas)"
    - "Skills necessárias listadas (/skills/...)"
    - "Golden queries para teste posterior"
    - "Product Specialist validou: 'Mantém escopo do requirement'"
    - "Tech Lead + Delivery Manager assinaram"
  
  consequence_if_rejected: "Volta para Tech Lead, simplifica scope ou refaz análise"

GATE-3:
  id: "GATE-3"
  name: "Tasks Approved"
  phase_before: "tasks.md"
  phase_after: "Implementation starts"
  owner_approver: "Tech Lead"
  sla_hours: 12
  sla_escalation: "Escalate to Tech Lead (pode simplificar scope)"
  input_artifact: "specs/{module}/tasks.md"
  output_decision: "[APPROVED | REQUEST_CHANGES | REJECTED]"
  
  approval_criteria:
    - "Arquivo existe: /specs/{module}/tasks.md"
    - "Baseado em plan.md aprovado (GATE-2)"
    - "Tasks IDs: NOVA-{module}.{sequence} (correto)"
    - "Nenhuma task > 13 story points"
    - "Cada task tem: description, AC testáveis, points, dependencies, skill"
    - "Skill referenciada: existe em /skills/ OU está em backlog"
    - "Sem ambiguidade (AC são testáveis, não vago)"
    - "Total points 30-40 (fits 1 sprint)"
    - "Dependency graph sem ciclos"
    - "Dev Sênior realizou refinamento pós-Copilot (se generated)"
    - "Tech Lead assinhou"
  
  consequence_if_rejected: "Volta para Dev Sênior, ajusta tasks e resubmete"

GATE-4:
  id: "GATE-4"
  name: "Code Review"
  phase_before: "Pull Request"
  phase_after: "Merge to cenário-1"
  owner_approver: "Tech Lead + Dev Sênior (if Dev Pleno)"
  sla_hours: 4
  sla_escalation: "Auto-escalation at 2h mark (pair review), 4h = escalate to Tech Lead"
  input_artifact: "Pull Request + CI Pipeline"
  output_decision: "[APPROVED | REQUEST_CHANGES | REJECTED]"
  
  approval_criteria:
    - "CI Pipeline PASSING: lint, build, test, coverage > 80%"
    - "Skill pattern followed (/skills/artifact/... padrão)"
    - "Sem console.log, debugger, TODO, FIXME"
    - "Comentários em lógica complexa (JSDoc, contexto)"
    - "Mensagens de erro descritivas (não '400')"
    - "SE toca RAG: golden queries testadas + fonte verificável"
    - "SE toca PROC-042: versão diferenciação testada"
    - "SE toca cargas perigosas: rejeição testada"
    - "SE toca SLAs: constraint validação testada"
    - "Code não viola /skills/foundation/typescript-conventions.md"
    - "Tech Lead assinhou como aprovador"
  
  consequence_if_rejected: "Dev makes commit fix, Tech Lead reviews again (2h SLA)"

GATE-5:
  id: "GATE-5"
  name: "Test Review"
  phase_before: "Test Results"
  phase_after: "Deploy Ready"
  owner_approver: "QA + Product Specialist"
  sla_hours: 48
  sla_escalation: "Can run parallel with next sprint if needed"
  input_artifact: "Test Results + Coverage Report + Golden Queries"
  output_decision: "[APPROVED | REQUEST_CHANGES | REJECTED]"
  
  approval_criteria:
    - "Coverage > 80% para código novo"
    - "5 Golden queries testadas contra chunks reais"
    - "CRITICAL: Toda resposta tem FONTE verificável (format: 'POL-001-A Seção X')"
    - "SE RAG: contradição PROC-042 v1 vs v2 testada (data-based)"
    - "SE cargas perigosas: resposta inclui POL-001-B + ramal 4500"
    - "SE SLAs: resposta não inventa tiers (Gold/Silver/Standard apenas)"
    - "Latência P95 < 2s em teste"
    - "Error rate < 0.1%"
    - "Product Specialist validou: 'Resposta atende requirement original'"
    - "QA + Product Specialist assinaram"
  
  consequence_if_rejected: "Volta antes deploy, QA ou Dev ajusta testes/código"

GATE-6:
  id: "GATE-6"
  name: "Deploy Ready"
  phase_before: "Staging Validated"
  phase_after: "Production"
  owner_approver: "Tech Lead + Delivery Manager"
  sla_hours: 4
  sla_escalation: "Rollback < 30 min if failure, on-call engineer escalates"
  input_artifact: "All previous GATES + Runbook + Monitoring"
  output_decision: "[APPROVED | BLOCKED]"
  
  approval_criteria:
    - "GATE-1 → 5 todos APPROVED"
    - "Infra ready: Azure Services, AI Search indexed (847 docs), OpenAI available"
    - "Runbook existe: /docs/runbooks/{module}-deploy.md (testado em staging)"
    - "Monitoring ativo: alertas P95 > 2s, error rate > 1%"
    - "Release notes publicadas: /docs/releases/{version}.md"
    - "Release notes enviadas: Slack + Email"
    - "Tech Lead + Delivery Manager assinaram"
  
  consequence_if_rejected: "Deploy agendado, timeline estendida"
```

### 3.3 How Agents Use Gate Definitions

**Rule:** Agents MUST execute gates in sequence; no skipping

**Workflow:**

```python
# Pseudo-code for agents following gates

GATES_SEQUENCE = [GATE-1, GATE-2, GATE-3, GATE-4, GATE-5, GATE-6]

def validate_gate(gate_id, artifact):
    """
    Validates artifact against gate criteria.
    Returns: {status: 'APPROVED|REQUEST_CHANGES|REJECTED', feedback: [...]}
    """
    gate = GATES[gate_id]
    
    # Check all criteria
    for criterion in gate.approval_criteria:
        if not check(artifact, criterion):
            return {status: 'REQUEST_CHANGES', reason: criterion}
    
    # All criteria passed
    return {status: 'APPROVED', timestamp: now()}

def advance_phase(gate_result):
    """
    Only advance if gate approved.
    """
    if gate_result.status == 'APPROVED':
        # Proceed to next phase
        return NEXT_PHASE
    else:
        # Block, notify owner
        notify_owner(gate_result.reason)
        return BLOCK

# Usage
gate_1_result = validate_gate('GATE-1', requirements_md)
if gate_1_result.status == 'APPROVED':
    proceed_to_plan_phase()
else:
    request_changes_from_product_specialist()
```

---

## 4. Communication Rules

### 4.1 Language Rules

**Rule:** Strict language segregation for different artifact types

**Specification:**

```
PORTUGUESE (português brasileiro):
  ✓ User-facing documents (README, user guides, how-tos)
  ✓ Status reports and project communication
  ✓ Specification documents (requirements, plans, tasks)
  ✓ Team documentation (runbooks, troubleshooting guides)
  ✓ Meetings notes and decisions
  ✓ Client communication and email

ENGLISH (US English, en-US):
  ✓ Code (function names, variables, comments)
  ✓ Git commits and PR descriptions
  ✓ ADR (Architecture Decision Records) and technical documentation
  ✓ API specifications and contracts
  ✓ Comments in code (especially complex logic)
  ✓ JSDoc / code documentation
  ✓ File and folder names

MIXED (Allowed only with explicit markers):
  ✓ Code with inline comments (code = English, comments = context language)
    Example:
      // Validar versão PROC-042 (v1 vs v2)
      if (orderDate < PROC_042_V2_CUTOFF) { // 01/12/2023
        multiplier = PROC_042_V1_MULTIPLIER;
      }

  ✓ Documentation with code examples (prose = Portuguese, code = English)
    Example:
      "A função chunker divide documentos em pedaços com 20% de sobreposição.
       
       ```typescript
       const chunks = chunkDocument(pdf, {overlap: 0.2, maxTokens: 1500});
       ```"

NOT ALLOWED (mixed without context):
  ✗ Function names in Portuguese (should be English)
  ✗ Variable names in Portuguese (should be English)
  ✗ Git commits in Portuguese (should be English)
  ✗ ADRs in Portuguese (should be English)
  ✗ API specs in Portuguese (should be English)
```

### 4.2 Status Report Format

**Rule:** Agents generating status reports MUST follow this format

**Specification:**

```
LOCATION:     Slack #novatech-status (daily 09:00 BRT)
FORMAT:       Portuguese
LENGTH:       4-6 bullet points max
FREQUENCY:    Daily (generated by Cowork automation)
AUDIENCE:     Team + Delivery Manager + Stakeholders

REQUIRED SECTIONS (in order):
1. ✓ Completed tasks (NOVA-X.Y IDs)
2. ⏳ In progress (NOVA-X.Y, owner, % done)
3. ⚠️ Blockers/Risks (if any)
4. 📊 Velocity (X/40 points done, on track/at risk)
5. 🚦 Gates (which gates passed, which in review)

TEMPLATE:
"
**Status Sprint [N] - [Module Name]**

✓ Concluído:
  • NOVA-1.1 (Setup Azure)
  • NOVA-1.2 (PDF extraction)

⏳ Em andamento:
  • NOVA-1.3 (Dev Sênior, 80% done)
  • NOVA-1.4 (queued, waiting 1.3 complete)

⚠️ Bloqueadores:
  • Nenhum no momento

📊 Velocidade:
  • 26/40 points (65%, on track)

🚦 Gates:
  • GATE-1: ✅ Aprovado (requirements)
  • GATE-2: ⏳ Em revisão (plan, 18h SLA remaining)
  • GATE-3: ⏳ Aguardando (tasks, after GATE-2)
"

RULES:
  ✗ Do NOT use English in status reports
  ✗ Do NOT include implementation details (save for docs)
  ✗ Do NOT mention drama or blame (professional tone)
  ✓ Do USE NOVA-X.Y format for task IDs
  ✓ Do REFERENCE gates explicitly
  ✓ Do INCLUDE emoji for visual parsing
```

### 4.3 Specification Document Language

**Rule:** Specification documents (requirements, plan, tasks) MUST be in Portuguese

**Specification:**

```
FILE:         specs/{module}/{type}.md
LANGUAGE:     Portuguese (Brasil)
AUDIENCE:     Team + Delivery Manager
EXAMPLES:     
  - requirements.md: "Visão Geral", "Histórias de Usuário", "Critérios de Aceitação"
  - plan.md: "Arquitetura", "Matriz de Risco", "Sequência de Implementation"
  - tasks.md: "Tasks", "Dependências", "Estimativas"

RULES:
  ✓ All user-facing specs in Portuguese
  ✓ Code examples inside specs can be English
  ✓ Tech terms can stay in English if clearer (e.g., "chunking", "embedding")
  ✗ Do NOT translate to English unless explicitly requested
  ✗ Do NOT use Portuguese field names in YAML/structured data (use English)

EXAMPLE (correct):
"
# Plano — Pipeline de Ingestão

## Arquitetura

Usaremos Azure AI Search para indexação de chunks.

\`\`\`typescript
const chunks = chunkDocument(pdf, {maxTokens: 1500});
\`\`\`
"
```

### 4.4 Code Comments Language

**Rule:** Code comments MUST explain WHY, and use context language

**Specification:**

```
Code:         English (variables, functions, classes)
Comments:     Use context language to explain WHY
Location:     //

RULES:
  ✓ Short in-line comments: Portuguese (explain local context)
    Example:
      // Validar se data é anterior a transição PROC-042 (01/12/2023)
      if (orderDate < CUTOFF_DATE) { ... }
  
  ✓ Block comments: Portuguese (explain algorithm/context)
    Example:
      // Algoritmo de chunking com sobreposição
      // 1. Dividir em chunks de 1500 tokens
      // 2. Adicionar 20% de sobreposição com chunk anterior
      // 3. Validar versão PROC-042 (v1 vs v2)
  
  ✓ JSDoc: English (API contract)
    Example:
      /**
       * Chunk document into overlapping segments
       * @param {Buffer} pdf - PDF content
       * @param {Object} options - {maxTokens, overlap}
       * @returns {Array<Chunk>} Chunked document
       */

  ✗ Do NOT translate code comments to English if explaining local logic
  ✗ Do NOT use Portuguese in JSDoc (use English)
  ✗ Do NOT comment obvious code ("i = i + 1" doesn't need comment)
```

### 4.5 Git Commit Messages

**Rule:** Git commits MUST follow conventional format in English

**Specification:**

```
Format:       {type}({scope}): {description}
Type:         [feat|fix|docs|refactor|test|chore]
Scope:        [module-slug]
Description:  English, imperative, < 72 chars
Body:         (optional) Explain WHY, not WHAT

REQUIRED in body if feature/fix:
  Issue: [describe problem]
  Solution: [describe solution]
  Impact: [what changed, who affected]
  Related: [NOVA-X.Y, ADR-NNNN, if applicable]

EXAMPLES (CORRECT):

feat(pipeline-ingestao): implement document chunking with overlap

Issue: Documents need to be split into manageable chunks for embedding
Solution: Implement chunking algorithm with 20% overlap (via tiktoken)
Impact: NOVA-1.2 complete, unblocks NOVA-1.3 (versioning)
Related: NOVA-1.2, specs/pipeline-ingestao/tasks.md

fix(query-endpoint): handle PROC-042 version differentiation

Issue: Responses not distinguishing PROC-042 v1 vs v2 based on date
Solution: Check orderDate < 2023-12-01 to select correct version
Impact: Removes ambiguity, fixes NOVA-2.3 AC validation
Related: NOVA-2.3, ADR-0003-proc-042-version-handling-metadata

docs(painel-web): add metric calculation runbook

Issue: Ops team needs to understand how metrics are calculated
Solution: Document calculation logic in /docs/runbooks/
Impact: Reduces support questions, improves transparency
Related: NOVA-5.4, NOVA-5.5

EXAMPLES (INCORRECT):
  "update stuff" (too vague)
  "feat: implement chunking em português" (Portuguese)
  "feat(pipeline-ingestao): implementando..." (gerund, Portuguese)
  "Implement document chunking" (missing type/scope)
```

---

## 5. Artifact Generation Rules for Agents

### 5.1 When Generating Specifications (requirements/plan/tasks)

**Rule:** Agents MUST validate against gate criteria before generating

**Specification:**

```
Before generating specifications, agents MUST:

1. Identify gate to validate against
   GATE-1 for requirements.md
   GATE-2 for plan.md
   GATE-3 for tasks.md

2. Extract ALL approval criteria from gate definition
   Use criteria from Section 3.2 (Validation Gates)

3. Generate artifact ensuring 100% of criteria are met
   Do NOT generate if criteria cannot be met

4. Include changelog in spec
   Format: > **Changelog:** v1.0 (YYYY-MM-DD) initial, {status}

5. Validate language (Portuguese for specs)
   Do NOT generate spec in English

EXAMPLE: Agent generating requirements.md

Agent thinks:
  "GATE-1 requires: 3+ user stories, AC testáveis, chunks referenced if RAG..."
  "This module is pipeline-ingestao (RAG), so must include chunks list"
  "AC must NOT use vague words like 'funciona bem'"
  "No TBD allowed"
  
Agent generates:
  - Requirements with 4 user stories (exceeds min of 3)
  - Each AC is testável (not vague)
  - References chunks from Anexo B
  - No TBD anywhere
  - Changelog: "v1.0 (2026-06-19) initial"

Agent validates:
  "Let me check all GATE-1 criteria... [passes all]"
  "Ready to submit for approval"
```

### 5.2 When Generating Tasks (tasks.md)

**Rule:** Agents generating tasks MUST use Copilot-assisted decomposition pattern

**Specification:**

```
Process for agents generating tasks.md:

1. Input: Validated plan.md (GATE-2 approved)

2. Decomposition:
   Use GitHub Copilot as copilot (not primary agent)
   Prompt: "Given this plan.md, decompose into NOVA-X.Y tasks"
   Copilot generates initial decomposition
   Agent refines (validates AC, dependencies, estimates)

3. Validation checklist (from GATE-3):
   ☐ Task IDs: NOVA-{module}.{sequence}
   ☐ No task > 13 points
   ☐ AC testáveis, not vague
   ☐ All dependencies explicit (no hidden cycles)
   ☐ All skills referenced (/skills/... or backlog)
   ☐ Total 30-40 points

4. Output format:
   Must match template in Section 2.2 (ADR Template)
   Language: Portuguese (except code examples)
   Changelog: v1.0 (generated by {agent-name} + refined)

5. Commit:
   git commit -m "feat(module-slug): generate tasks decomposition
   
   Basado: plan.md v1.0 (GATE-2 approved)
   Process: Copilot decomposition + manual refinement
   Validation: All GATE-3 criteria met
   Related: specs/module/plan.md"
```

### 5.3 When Generating Status Reports (Cowork)

**Rule:** Agents generating status reports MUST use exact template

**Specification:**

```
Agent (Cowork) generating status:

1. Input: Azure DevOps board state + GitHub metrics

2. Extract data:
   - Completed tasks (moved to Done column)
   - In-progress (Active status, % from commit history)
   - Blockers (tagged Blocked)
   - Sprint velocity (sum of completed story points / 40)
   - Gates status (Azure DevOps tags)

3. Generate report:
   Use template from Section 4.2
   Language: Portuguese
   Format: Slack message
   Length: 4-6 bullets max

4. Post:
   Channel: #novatech-status
   Time: 09:00 BRT daily
   Frequency: Every business day

5. Validation:
   ✓ Uses emoji for parsing
   ✓ References NOVA-X.Y correctly
   ✓ Shows gate status
   ✓ No details (high-level only)
   ✓ Professional tone
```

---

## 6. Module-Specific Rules

### 6.1 NOVA-1: pipeline-ingestao

**Special rules for agents working on module 1:**

```
Module context:
  - Ingests 847 documents from NovaTech
  - Critical: Multiple versions of PROC-042 (v1 before 2023-12-01, v2 after)
  - Critical: POL-001-B excludes dangerous materials from standard returns
  - SLA-2024 defines tiers: Gold, Silver, Standard (no Platinum)

Naming rule for tasks:
  NOVA-1.1, NOVA-1.2, ... NOVA-1.7

Critical constraints agents MUST enforce:
  ☐ AC must reference metadata "versão" + "vigência_desde" for PROC-042
  ☐ AC must explicitly handle cargas perigosas (POL-001-B)
  ☐ AC must validate SLA tiers (only Gold/Silver/Standard, reject Platinum)
  ☐ Chunks must include source document and chunk index

If agent detects omission of these constraints:
  REJECT spec generation until constraints added

Example validation:
  Agent reads requirements.md for NOVA-1
  Agent checks: "Does it mention PROC-042 version handling?" NO → REJECT
  Agent checks: "Does it mention POL-001-B handling?" NO → REJECT
  Agent regenerates with constraints
```

### 6.2 NOVA-2: query-endpoint

**Special rules for agents working on module 2:**

```
Module context:
  - Searches indexed documents via RAG
  - CRITICAL: Response MUST include source (format: "POL-001-A Seção 3")
  - Depends on NOVA-1 output (chunks from pipeline-ingestao)
  - Must differentiate PROC-042 versions based on date

Naming rule:
  NOVA-2.1, NOVA-2.2, ...

Critical constraints:
  ☐ AC must include validation: source is retrievable
  ☐ AC must test version differentiation (query date → correct PROC version)
  ☐ AC must test SLA constraints (response < 2s P95)
  ☐ AC must reject hallucinations (fake sources)

Agent validation:
  If spec doesn't mention "source verificável" → REJECT
  If spec doesn't mention version differentiation → REJECT
```

### 6.3 NOVA-3: feedback-api

**Special rules for agents working on module 3:**

```
Module context:
  - Logs user feedback when response is wrong
  - Feeds into continuous improvement loop
  - Data stores in Cosmos DB

Naming rule:
  NOVA-3.1, NOVA-3.2, NOVA-3.3

Standard constraints (no special ones)
  Use default gate criteria
```

### 6.4 NOVA-4: teams-bot

**Special rules for agents working on module 4:**

```
Module context:
  - Conversational interface in Microsoft Teams
  - Connects to query-endpoint (NOVA-2) for answers

Naming rule:
  NOVA-4.1, NOVA-4.2, ... NOVA-4.5

Critical constraints:
  ☐ AC must test Teams SDK integration
  ☐ AC must handle long responses (Teams char limit)
  ☐ AC must preserve conversation context

Agent validation:
  If spec doesn't mention Teams SDK → REJECT
  If spec doesn't mention context preservation → REJECT
```

### 6.5 NOVA-5: painel-web

**Special rules for agents working on module 5:**

```
Module context:
  - Dashboard UI for metrics and chat history
  - React + d3 for visualization
  - Reads from backend APIs

Naming rule:
  NOVA-5.1, NOVA-5.2, ... NOVA-5.6

Critical constraints:
  ☐ AC must specify accessibility (WCAG standard)
  ☐ AC must test metric calculations
  ☐ AC must handle mobile responsiveness

Agent validation:
  If spec doesn't mention accessibility → REJECT
  If spec doesn't mention mobile → REJECT
```

---

## 7. Error Handling for Agents

### 7.1 What to Do When Spec is Invalid

**Rule:** Agents MUST NOT proceed if spec violates rules

**Specification:**

```
If agent detects violation of ANY rule in this document:

1. IDENTIFY the violation
   Log: "VIOLATION: {rule number} — {specific issue}"

2. DO NOT PROCEED
   Do NOT generate artifact
   Do NOT advance phase

3. NOTIFY HUMAN
   Message to owner (via Slack/Azure DevOps):
   "⚠️ Cannot generate {artifact}: {violation reason}
    
    Expected: {rule requirement}
    Found: {actual state}
    
    Please fix and resubmit."

4. WAIT FOR HUMAN FIX
   Do not retry automatically
   Wait for human to acknowledge and fix

5. EXAMPLES of violations that trigger BLOCK:

   ❌ requirements.md for NOVA-1 without PROC-042 reference
       → Block: "Module 1 MUST include PROC-042 v1 vs v2 handling"
   
   ❌ Task ID "NOVA-pipeline-ingestao-1" (wrong format)
       → Block: "Task ID must be NOVA-1.1 (not NOVA-pipeline-ingestao-1)"
   
   ❌ AC "funciona bem" (vague)
       → Block: "AC must be testável, 'funciona bem' is too vague"
   
   ❌ git commit in Portuguese
       → Block: "Git commits must be in English format (type(scope): desc)"
   
   ❌ Specification in English (should be Portuguese)
       → Block: "specs/{module}/{type}.md must be in Portuguese"
```

---

## 8. Summary for Agents

**Quick Reference:**

```
IF YOU ARE AN AI AGENT:

1. NAMING: Use NOVA-{module}.{seq}, {type}({scope}): {desc}
2. GATES: Follow GATE-1 → GATE-6 in sequence, check all criteria
3. LANGUAGE: Portuguese for specs, English for code/git
4. DECISIONS: Every technical choice → ADR in /docs/adr/
5. STATUS: Use Slack template, Portuguese, daily 09h
6. VALIDATION: Check rules BEFORE generating, not after
7. ERROR: If violation detected, STOP and notify human

CONTACT: Tech Lead (@tech-lead) if questions
REFERENCE: Full rules in this section "Project Management Rules"
```

---

**Version:** 1.0  
**Last Updated:** 2026-06-18  
**Format:** Machine-readable specification  
**For questions:** @tech-lead in Slack #novatech-dev
