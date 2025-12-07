# AIOBoss: Context Engineering Framework
## Single Source of Truth (SSOT) para Escritórios Agenticos

**ID Principal:** 071225-200000  
**Versão:** 1.0.0 (Foundation Layer)  
**Status:** Active Development  
**Última Atualização:** 2024-12-07 20:00 UTC-3

---

## 🎯 DEFINIÇÃO FUNDACIONAL

### O Que É AIOBoss

AIOBoss é um **conjunto de prompt templates + role definitions distribuído** que, quando copiado para qualquer projeto, transforma Copilot/Claude/Cursor em um **escritório agentico virtual autossuficiente**.

**Não é:**
- ❌ Sistema de automação complexo
- ❌ Webhooks ou orquestração de microserviços
- ❌ Database ou vector store centralizado
- ❌ Plataforma proprietária lock-in

**É:**
- ✅ Arquivos markdown + prompts estruturados
- ✅ CONTEXT.md como memória persistente
- ✅ Outputs no filesystem (versionados em git)
- ✅ Agnóstico de plataforma (funciona em VSCode, Cursor, GitHub Copilot, Claude)

### Princípios Fundadores

```text
DRY:   Don't Repeat Yourself
KISS:  Keep It Simple Stupid
SSOT:  Single Source of Truth

+ Retórica em 3 Pilares:
  - Ethos:  Credibilidade (agente sabe seu domínio)
  - Pathos: Empatia (entender o receptor da mensagem)
  - Logos:  Lógica (sequência ordenada de raciocínio)
```

---

## 🏗️ ARQUITETURA CONCEITUAL

### O Padrão: "Self-Documenting Agentic System"

```text
Projeto Novo (clonado)
│
├── .aioboss/                          ← Estrutura copiada do template
│   ├── agent-architecture.md          ← Roles definidas
│   ├── copilot-agent-prompt.md        ← SSOT (instruções operacionais)
│   ├── copilot-agent-prompt-template.md ← Template para novos agentes
│   ├── GITHUB_TEMPLATE/agents/        ← Definições de agentes
│   │   ├── context-engineer.agent.md
│   │   ├── task-planner.agent.md
│   │   ├── dev-agent.agent.md
│   │   ├── product-manager.agent.md
│   │   └── ...
│   ├── CONTEXT.md                     ← Memória persistente (AUTO-UPDATED)
│   └── chunks/                        ← RAG index (markdown files)
│
├── README.md                          ← Documentação padrão
├── package.json                       ← Tech stack
└── src/                               ← Código do projeto
```

### Os 4 Agentes Core (MVP)

| Agente | Responsabilidade | Quando Acionado |
|--------|------------------|-----------------|
| **Context Engineer** | Mapear/manter SSOT, CONTEXT.md, RAG | Você: "update context", "map project" |
| **Task Planner** | Quebrar requisitos em sub-tasks | Você: "como implementar feature X?" |
| **Dev Agent** | Implementar código, testes, PRs | Task Planner → Dev Agent (chain) |
| **Head-of-Office** | Aprovação final, governança | Antes de merge crítico |

Agentes FUTURE (Phase 2):
- Product Manager (OKRs, backlog)
- UX Designer (acessibilidade, design)
- Test Agent (QA, regressão)
- Docs Agent (documentação automática)

---

## 🔄 FLUXO END-TO-END (Cenário Real)

### FASE 1: Setup (Você, Humano)

```bash
# 1. Clona projeto novo (ou existente)
git clone https://github.com/seu-usuario/novo-projeto
cd novo-projeto

# 2. Copia estrutura aioboss
cp -r ~/aioboss/.aioboss ./.aioboss

# 3. Abre em VSCode/Cursor
code .
```

### FASE 2: Bootstrap (Copilot, Semi-Automático)

```text
Você digita no Copilot Chat:
"""
Bootstrap agentico. 

Siga:
1. Leia .aioboss/agent-architecture.md
2. Leia .aioboss/GITHUB_TEMPLATE/agents/*.agent.md
3. Escanear repositório e criar .aioboss/CONTEXT.md
4. Confirme quando pronto

Princípios: DRY, KISS, SSOT
Retórica: Ethos, Pathos, Logos
"""

Copilot (agindo como Context Engineer):
> read_file: .aioboss/agent-architecture.md
> read_file: .aioboss/GITHUB_TEMPLATE/agents/context-engineer.agent.md
> read_file: README.md, package.json
> grep_search: "export", "import" (mapear arquitetura)

Copilot output:
"✅ Projeto mapeado. 8 módulos, stack: Next.js + PostgreSQL"
"📋 CONTEXT.md criado em .aioboss/CONTEXT.md"
"🔍 5 chunks indexados em .aioboss/chunks/"
"Aguardando próximas tasks..."
```

### FASE 3: Operação (Você + Copilot, Iterativo)

```text
Você:
"Preciso implementar autenticação OAuth2"

Copilot (assumindo role de Task Planner):
"""
📋 Plano de Execução:

1. [Context Engineer] Mapear auth atual
   - read_file: src/auth/
   - grep_search: "login", "session"
   - Atualizar CONTEXT.md com estado

2. [Dev Agent] Implementar OAuth2
   - Instalar @auth/nextjs, @next-auth/core
   - Criar [...nextauth].ts
   - Implementar callbacks

3. [Dev Agent] Criar testes
   - Test files: src/auth/__tests__/oauth.test.ts
   - Coverage > 80%

4. [Context Engineer] Sincronizar CONTEXT.md
   - Adicionar OAuth2 à seção "Auth Architecture"
   - Atualizar chunks/

Quer que eu comece pelo passo 1?
"""

Você: "Sim"

Copilot (agora como Context Engineer):
> read_file: src/auth/*
> grep_search: "authentication", "JWT", "session"
> 
> Encontrei:
> - src/auth/jwt.ts (JWT handler)
> - src/auth/session.ts (session management)
> - src/middleware.ts (auth middleware)
>
> Vou atualizar CONTEXT.md...
>
> apply_patch: .aioboss/CONTEXT.md
> create_file: .aioboss/chunks/auth-current-state.md
>
> ✅ Contexto sincronizado
> Próximo: Dev Agent pode iniciar implementação
```

### FASE 4: Implementação (Dev Agent)

```text
Copilot (como Dev Agent):
> read_file: .aioboss/CONTEXT.md
> read_file: .aioboss/chunks/auth-current-state.md (RAG)
>
> Entendi. Sistema atual usa JWT + session store.
> Vou adicionar OAuth2 mantendo compatibilidade...
>
> create_file: src/auth/oauth.ts
> apply_patch: src/auth/[...nextauth].ts
> create_file: src/auth/__tests__/oauth.test.ts
> apply_patch: src/middleware.ts
>
> 📝 Pronto. Aqui está o diff:
> [mostra apply_patch diffs]
>
> ✅ Testes passam
> ✅ TypeScript OK
> 
> Quer que eu crie PR draft?
```

### FASE 5: Revisão (Você, Humano)

```markdown
Você:
"Revisa diffs acima"

[Você lê os patches propostos no editor]

Você:
"Aprovo. Implementa."

Copilot:
> apply_patch: todos os arquivos
> git add .
> git commit -m "feat: add OAuth2 authentication"
> git push origin feature/oauth2

Copilot:
"✅ Feature implementada e sincronizada"
"📋 CONTEXT.md atualizado com OAuth2"
"🔗 PRonto para code review/merge"
```

---

## 📋 OUTPUTS: O QUE FICA SALVO

Após executar o fluxo acima, você tem:

```text
.aioboss/
├── CONTEXT.md                    ← Estado atual (sempre sincronizado)
├── chunks/
│   ├── arch-overview.md          ← RAG index
│   ├── auth-current-state.md     ← Mapeamento de auth
│   ├── auth-oauth2-impl.md       ← Implementação OAuth2
│   └── ...
└── outputs/                      ← Histórico (opcional)
    └── 2024-12-07-oauth2-implementation.md

src/
├── auth/
│   ├── oauth.ts                  ← Novo arquivo
│   ├── [...nextauth].ts          ← Modificado
│   ├── jwt.ts                    ← Unchanged
│   └── __tests__/
│       └── oauth.test.ts         ← Novo arquivo

git log:
> feat: add OAuth2 authentication
```

**Tudo versionado em git. Zero lock-in.**

---

## ⚙️ COMO CONTEXT ENGINEER FUNCIONA (Deep Dive)

### Responsabilidades Principais

```yaml
Context Engineer:
  Owner: SSOT, RAG, CONTEXT.md, chunking strategy
  
  Ativação:
    - User request: "map project", "update context", "explain architecture"
    - Autre agent needs context refresh
    - Auto-detect: semantic_search returns low coverage
  
  Workflow:
    1. read_file + grep_search → mapear projeto
    2. Identificar gaps (CONTEXT.md desatualizado, docs inconsistentes)
    3. Produzir plano com passos atômicos
    4. Fragmentar contexto em chunks (JSON + markdown)
    5. apply_patch → gerar diffs (nunca push sozinho)
    6. Output estruturado (JSON/Markdown)
    7. Escalar ao Supervisor se alteração crítica
  
  Tools:
    ✅ file_search, read_file, grep_search, semantic_search
    ✅ apply_patch, create_file, create_directory
    ✅ runTests, run_in_terminal, get_errors
    ❌ mcp_github_* (só com aprovação explícita)
  
  Output Format:
    {
      "objective": "...",
      "chunks": [
        {"id": "c1", "summary": "...", "source": "..."}
      ],
      "plan": [
        {"step": 1, "description": "...", "tool": "..."}
      ],
      "tests": ["..."],
      "prChecklist": ["typecheck", "lint", "tests"]
    }
  
  Success Criteria:
    ✅ semantic_search retorna resultados relevantes < 250ms
    ✅ 100% de mudanças documentadas antes de PR
    ✅ 100% de mudanças críticas com aprovação manual
    ✅ Zero inconsistências (CONTEXT.md ↔ código)
```

---

## 📐 ESTRUTURA DO CONTEXT.MD (Template)

# CONTEXT.md

**Auto-updated by:** Context Engineer  
**Last scan:** 2024-12-07 20:00 UTC  
**Status:** ✅ Synchronized

## Project Identity

| Key | Value |
|-----|-------|
| Name | [PROJECT_NAME] |
| Repository | [GITHUB_URL] |
| Tech Stack | [STACK] |
| Node.js | ^20.0.0 |
| React | ^18.0.0 |
| Phase | Prototype / MVP / Production |

## Current State

### Codebase Overview
- **Total Files:** 234
- **Modules:** 18
- **Tests:** 87 (coverage: 72%)
- **Last Commit:** [HASH] ([MESSAGE])
- **Active Branch:** main

### Architecture Summary
[AUTO-GENERATED from code structure]

### Critical Blockers
- None current

### Next Development Steps
1. Implement feature X (estimated: 3 days)
2. Deploy to staging (estimated: 1 day)

## RAG Chunks Index

All chunks stored in `.aioboss/chunks/`

| Chunk ID | Summary | Source | Keywords |
|----------|---------|--------|----------|
| c1-arch-overview | Core architecture design | packages/editor/src/Editor.ts | editor, core, architecture |
| c2-auth | Authentication flow | src/auth/ | auth, oauth2, jwt |
| c3-db-schema | Database schema | schema.prisma | database, tables, relations |

## Team & Roles

| Role | Owner | Status |
|------|-------|--------|
| Context Engineer | Copilot | Active |
| Dev Agent | Copilot | Active |
| Task Planner | Copilot | Active |
| Head-of-Office | Human | Active |
| Product Manager | TBD | Pending |

## Decision Log (ADR-style)

### ADR-001: Use OAuth2 instead of custom auth
- **Date:** 2024-12-07
- **Status:** Approved
- **Rationale:** Industry standard, better security
- **Impact:** Refactor existing JWT code

## Glossário de Domínio

| Termo | Significado |
|-------|-------------|
| SSOT | Single Source of Truth |
| Context Engineer | Agente que mapeia e mantém CONTEXT.md |
| Chunk | Fragmento de contexto indexado para RAG |

---

**Próxima atualização esperada:** 2024-12-08 (ou quando Context Engineer for acionado)

```markdown
## 🚀 PRÓXIMOS ARTEFATOS A CRIAR (Phase 1)

### Artefato 1: Bootstrap Prompt (Você digita isso)

```markdown
# bootstrap-prompt.md

Salve este arquivo e cole no Copilot quando clonar novo projeto.

---

## Bootstrap Prompt (COPY-PASTE)

"""
Você é um sistema agentico multi-role para este repositório.

### Descoberta Inicial
1. Leia: .aioboss/agent-architecture.md
2. Leia: .aioboss/copilot-agent-prompt.md
3. Leia: .aioboss/GITHUB_TEMPLATE/agents/*.agent.md

### Seu Primeira Tarefa (como Context Engineer)
- Escanear este repositório (README.md, package.json, src/)
- Criar .aioboss/CONTEXT.md com estado atual
- Indexar conteúdo em .aioboss/chunks/
- Confirme quando pronto: "✅ Sistema agentico bootstrapped"

### Princípios Operacionais
- DRY: Não repita informações
- KISS: Mantenha simples
- SSOT: .aioboss/CONTEXT.md é fonte única de verdade
- Ethos: Seja credível no seu domínio
- Pathos: Entenda o receptor
- Logos: Explique raciocínio lógico

### Restrições
- Nunca push/merge sem aprovação humana
- Sempre prepare apply_patch diffs para revisão
- Escale decisões críticas (CI/CD, API pública, deploy)

### Próximo: Aguarde instrução do usuário
Quando pronto, responda com status e aguarde.
"""
```

### Artefato 2: Context Engineer Prompt (Pronto para Usar)

```markdown
# context-engineer-prompt.md

Use este prompt quando quiser que Copilot atue como Context Engineer.

---

Você é o Sub-Agente: **Engenheiro de Contexto** (Context Engineer) — Nível: Sênior.

### Seu Papel
Capturar, organizar e manter o Single Source of Truth (SSOT) deste repositório.

### Ativação
Você é acionado quando:
- User pede: "map project", "update context", "what's current state?"
- Outro agente precisa de refresh de contexto
- semantic_search retorna baixa cobertura

### Seus Passos (sempre nessa ordem)

1. **Descoberta**
   - read_file: README.md, package.json, src/ (estrutura geral)
   - grep_search: palavras-chave importantes (auth, db, api)
   - Identificar gaps: o que falta documentação? O que está desatualizado?

2. **Geração de Plano**
   - Produzir Markdown com objetivo + passos atômicos
   - Listar ferramentas necessárias
   - Listar testes/validações (com comandos exatos)
   - Incluir checklist de PR

3. **Fragmentação (Chunking)**
   - Dividir contexto em blocos nomeados
   - Cada chunk tem: ID + summary + source + keywords
   - Salvar em .aioboss/chunks/ (arquivo markdown)

4. **Preparação de Diffs**
   - Se precisa editar arquivos, use apply_patch
   - Nunca aplique sem aprovação (sempre prep diffs primeiro)
   - Incluir contexto antes/depois

5. **Output Final**
```json
{
  "objective": "Mapear autenticação atual",
  "chunks": [
    {
      "id": "c2-auth",
      "summary": "OAuth2 + JWT integration",
      "source": "src/auth/",
      "keywords": ["oauth2", "jwt", "session"]
    }
  ],
  "plan": [
    {
      "step": 1,
      "description": "Scan auth files",
      "tool": "read_file + grep_search"
    }
  ],
  "tests": [
    "cd . && yarn test src/auth --coverage"
  ],
  "prChecklist": [
    "yarn typecheck",
    "yarn lint",
    "tests passed"
  ]
}
```

6. **Escalation**
   - Se alteração toca API pública, CI/CD, deploy → escale ao Head-of-Office

### Restrições (NÃO QUEBREM)
- ❌ Não faça push/merge sozinho
- ❌ Não exponha credenciais/secrets
- ❌ Não aplique patches sem aprovação
- ❌ Não modifique CI/CD sem aprovação explícita

### Sucesso = Quando
✅ semantic_search encontra contexto em < 250ms
✅ Todas mudanças estão documentadas
✅ Chunks estão indexados em .aioboss/chunks/
✅ CONTEXT.md reflete estado atual do código

```markdown

### Artefato 3: Exemplo End-to-End Documentado

```markdown
# example-workflow-oauth2.md

## Cenário: Implementar OAuth2

### Pré-requisitos
- Projeto clonado com .aioboss/ copiado
- Copilot bootstrapped (rodou bootstrap-prompt)
- CONTEXT.md criado e sincronizado

### Passo 1: Você inicia no Copilot

Input (você digita):
"""
Preciso adicionar autenticação OAuth2. 
Qual é o plano?
"""

### Passo 2: Task Planner responde

Output (Copilot como Task Planner):
"""
📋 Plano de Execução:

1. **Context Engineer** → Mapear auth atual
   - Escanear src/auth/
   - Atualizar CONTEXT.md
   - Indexar chunks/auth-current-state.md

2. **Dev Agent** → Implementar OAuth2
   - Install: @auth/nextjs, @next-auth/core
   - Create: src/auth/oauth.ts
   - Update: src/auth/[...nextauth].ts
   - Add: middleware integration

3. **Dev Agent** → Criar testes
   - File: src/auth/__tests__/oauth.test.ts
   - Coverage: >80%

4. **Context Engineer** → Sincronizar CONTEXT.md
   - Add OAuth2 architecture
   - Update chunks/

Quer que eu comece?
"""

### Passo 3: Você aprova

Input (você):
"""
Sim, comece pelo passo 1
"""

### Passo 4: Context Engineer executa

Copilot (agindo como Context Engineer):
"""
🔍 Mapeando auth atual...

> read_file: src/auth/jwt.ts
> read_file: src/auth/session.ts
> grep_search: "authentication", "JWT"

Encontrei:
- JWT token generation + validation (jwt.ts)
- Session store (Redis) (session.ts)
- Middleware (middleware.ts)

📝 Atualizando CONTEXT.md...
✅ CONTEXT.md atualizado
📊 Chunk auth-current-state.md criado

Próximo: Dev Agent pode iniciar.
"""

### Passo 5: Dev Agent implementa

Copilot (agindo como Dev Agent):
"""
💻 Implementando OAuth2...

> read_file: .aioboss/CONTEXT.md
> read_file: .aioboss/chunks/auth-current-state.md

Entendi. Sistema atual:
- JWT tokens com Redis session store
- Middleware checks auth
- No OAuth integration yet

Vou adicionar OAuth2 mantendo compat...

create_file: src/auth/oauth.ts
[código OAuth2]

apply_patch: src/auth/[...nextauth].ts
[diff mostrando onde adicionar]

create_file: src/auth/__tests__/oauth.test.ts
[testes para OAuth2]

apply_patch: src/middleware.ts
[integração no middleware]

✅ Testes passam
✅ TypeScript OK
✅ Lint OK

📋 Aqui estão os diffs para sua aprovação:
[mostra apply_patch diffs]

Quer que eu aplique?
"""

### Passo 6: Você aprova

Input (você):
"""
Revisa diffs acima... aprovo, implementa
"""

Copilot:
"""
✅ Código aplicado
✅ CONTEXT.md atualizado com OAuth2
✅ Chunks sincronizados
🎉 Feature implementada!

Status:
- Arquivos modificados: 4
- Testes: 23 passed
- TypeScript: no errors
- Lint: no errors

Pronto para merge!
"""

### Resultado Final

.aioboss/
├── CONTEXT.md (atualizado com OAuth2)
├── chunks/
│   ├── auth-current-state.md (incluindo OAuth2)
│   └── ...

src/auth/
├── oauth.ts (novo)
├── [...nextauth].ts (modificado)
├── jwt.ts (unchanged)
├── session.ts (unchanged)
└── __tests__/
    └── oauth.test.ts (novo)

git status:
M  src/auth/[...nextauth].ts
M  src/middleware.ts
M  .aioboss/CONTEXT.md
A  src/auth/oauth.ts
A  src/auth/__tests__/oauth.test.ts

**Tudo no git. Rastreável. Zero lock-in.**
"""
```

---

## 🎯 MÉTRICAS DE SUCESSO

Você saberá que AIOBoss funciona quando:

✅ Novo dev clona projeto → entende arquitetura em < 5 minutos
✅ Agentes NÃO alucinam (usam CONTEXT.md como memória)
✅ Feature inteira delegada a Copilot sem supervisão constante
✅ CONTEXT.md NUNCA fica desatualizado (sync automático)
✅ Documentação é código (não arquivo separado)
✅ Zero dependência de plataforma (é só markdown + prompts)
✅ Histórico completo em git (auditável)

---

## 📦 O QUE CRIAR NEXT (Prioridade)

### Tier 1 (CRÍTICO - Próximas horas)

- [ ] **bootstrap-prompt.md** — Prompt que você digita para bootstrap
- [ ] **context-engineer.agent.md (COMPRESSED)** — Role definition compactada
- [ ] **CONTEXT.md template** — Estrutura que agentes usam
- [ ] **example-workflow-oauth2.md** — Caso real documentado

### Tier 2 (IMPORTANTE - Próximas 24h)

- [ ] **task-planner.agent.md (COMPRESSED)** — 2º agente core
- [ ] **dev-agent.agent.md (COMPRESSED)** — 3º agente core
- [ ] **head-of-office.agent.md (COMPRESSED)** — Governança
- [ ] **Integration guide** — Como agentes se comunicam

### Tier 3 (NICE-TO-HAVE - Próximas semana)

- [ ] **Simulation suite** — Exemplos executáveis
- [ ] **RAG chunking strategy** — Detalhes técnicos
- [ ] **CI/CD bootstrap script** — Automação inicial
- [ ] **Multi-project orchestration** — Quando você tem múltiplos repos

---

## 🔗 REFERÊNCIAS INTERNAS

**Documentos relacionados neste workspace:**

- `workspace-prompt-mestre.md` — Sistema de IDs + SSOT geral
- `preferencias-usuario.md` — Seu estilo de comunicação
- `glossario-dominio.md` — Terminologia do seu projeto

**Repositórios:**

- [aiob3/aioboss](https://github.com/aiob3/aioboss) — Template principal
- [tldraw/tldraw](https://github.com/tldraw/tldraw) — Inspiração (CONTEXT.md pattern)

---

## ✋ CHECKPOINT

**Este documento é o SSOT de AIOBoss.**

Antes de criar os artefatos Tier 1, **confirme:**

- [ ] Definição está 100% correta?
- [ ] Padrão "self-documenting agentic system" faz sentido?
- [ ] Fluxo end-to-end é viável?
- [ ] Os 4 agentes core são suficientes para MVP?
- [ ] Estrutura do CONTEXT.md atende suas necessidades?

**Se tudo está OK:** Pronto para criar **bootstrap-prompt.md** e **context-engineer.agent.md (COMPRESSED)**.

---

**Versão Next:** 1.1.0 (após feedback)  
**Última Modificação:** 2024-12-07 20:00 UTC-3  
**Por:** Analysis and Documentation System
