# AIOBoss: Context Engineering Framework
## Single Source of Truth (SSOT) para Escritórios Agenticos

**ID Principal:** 071225-212900  
**Versão:** 1.1.0 (Fireman Integration Layer)  
**Status:** Ready for Tier 1 Creation  
**Última Atualização:** 2024-12-07 21:29 UTC-3

---

## 🚨 PROBLEMA REAL QUE AIOBOSS RESOLVE

### O Cenário: Solo Founder em Caos

```
Timeline de um Solo Founder típico:

Dia 1-7:      ✅ Constrói MVP em Lovable/Replit/VibeCode
Dia 8-15:     🤔 "Como eu organizo isso?"
Dia 16-30:    😰 "Perdi o mapa da minha própria arquitetura"
Dia 31-60:    💥 "Preciso de um Dev Team, mas não tenho orçamento"
Dia 61+:      💀 Projeto travado. Débito técnico insurmontável.

Raiz do Problema:
├─ Projeto cresceu DESORDENADO (sem estrutura inicial)
├─ Documentação não existe (ou está desatualizada)
├─ Contexto distribuído em N arquivos desconexos
├─ Solo founder = 0 knowledge transfer
└─ Copilot/Claude alucinam porque falta MEMÓRIA PERSISTENTE
```

### O Cenário AIOBoss Intervém: "Fireman Mode"

```
Você está em CAOS. Você:
1. Clona seu projeto existente no VSCode
2. Copia .aioboss/ para dentro do repo
3. Digita no Copilot: "Carregue os dados agênticos do #aioboss"
4. Copilot (agora FIREMAN) assume as rédeas
5. Em 30 minutos: Projeto mapeado, organizado, governado

Resultado:
├─ ✅ Você entende sua própria arquitetura novamente
├─ ✅ Copilot tem MEMÓRIA (CONTEXT.md)
├─ ✅ Agentes trabalham EM HARMONIA (não alucinam)
├─ ✅ Você passa de "caos solo" a "virtual dev team governado"
└─ ✅ Pronto para escalar ou contratar com contexto claro
```

---

## 🎯 DEFINIÇÃO FUNDACIONAL (ATUALIZADA)

### O Que É AIOBoss / Fireman

AIOBoss (codinome: **Fireman**) é um **sistema de governança agentica self-contained** que, quando copiado para qualquer projeto (novo OU em andamento, organizado OU em caos), transforma Copilot/Claude/Cursor em um **virtual dev team** com:

- ✅ Memória persistente (CONTEXT.md = SSOT)
- ✅ Estrutura de governança clara (agentes com roles definidos)
- ✅ Capacidade de mapear caos em 30 minutos
- ✅ Auto-sincronização (CONTEXT.md sempre atualizado)
- ✅ Zero lock-in (é só markdown + prompts)
- ✅ Agnóstico de plataforma (VSCode, Cursor, GitHub Copilot, Claude)

**O diferencial:** AIOBoss não é um "boilerplate bonito". É um **padrão de resgate** para projetos órfãos, desordenados ou negligenciados.

---

## 🏗️ ARQUITETURA CONCEITUAL (ATUALIZADA)

### O Padrão: "Self-Documenting Agentic System with Memory"

```
Projeto Novo OU Em Andamento (Caos ou Ordem)
│
├── .aioboss/                          ← INTELIGÊNCIA AUTOCONTIDA
│   ├── agent-architecture.md          ← Roles + governança
│   ├── copilot-instructions.md        ← MASTER PROMPT (SSOT operacional)
│   ├── GITHUB_TEMPLATE/agents/        ← Definições de agentes
│   │   ├── context-engineer.agent.md  ← "Mapeie meu caos"
│   │   ├── task-planner.agent.md      ← "Organize em tarefas"
│   │   ├── dev-agent.agent.md         ← "Implemente"
│   │   └── head-of-office.agent.md    ← "Aprove"
│   ├── CONTEXT.md                     ← MEMÓRIA PERSISTENTE (Auto-updated)
│   └── chunks/                        ← RAG index (markdown files)
│
├── .github/
│   └── copilot-instructions.md        ← Instrução nativa VSCode (referencia .aioboss/)
│
├── README.md                          ← Documentação padrão
├── package.json                       ← Tech stack
└── src/                               ← Seu código
```

### Os 4 Agentes Core (MVP)

| Agente               | Responsabilidade                        | Acionado Quando                  |
| -------------------- | --------------------------------------- | -------------------------------- |
| **Context Engineer** | Mapear caos → CONTEXT.md, SSOT, RAG     | "map project", "update context"  |
| **Task Planner**     | Quebrar requisitos → sub-tasks          | "como implementar feature X?"    |
| **Dev Agent**        | Implementar código, testes, PRs         | Task Planner → Dev Agent (chain) |
| **Head-of-Office**   | Aprovação final, governança, escalações | Antes de merge crítico           |

---

## 🔄 FLUXO END-TO-END: FIREMAN MODE (Resgate)

### FASE 0: O Ponto de Partida (Seu Cenário Real)

```
Você está aqui:
├─ Projeto em Lovable/Replit/VibeCode (ou VSCode local)
├─ 30-60 dias de desenvolvimento
├─ Código cresceu desordenado
├─ Você perdeu o mapa mental
├─ Copilot/Claude alucinam porque falta contexto
└─ Você precisa de ajuda AGORA, não "em 2 semanas"
```

### FASE 1: Setup (Você, Humano - 5 minutos)

```bash
# 1. Clona seu projeto existente (OU abre local)
git clone https://github.com/seu-usuario/seu-projeto
cd seu-projeto

# 2. Copia estrutura aioboss
cp -r ~/aioboss/.aioboss ./.aioboss

# 3. Abre em VSCode
code .
```

### FASE 2: Fireman Activation (Copilot, Automático - 30 minutos)

```
Você digita no Copilot Chat:
"""
🚨 ACTIVATE FIREMAN MODE

Carregue os dados agênticos do #aioboss.

Siga:
1. Leia: .aioboss/agent-architecture.md
2. Leia: .aioboss/copilot-instructions.md
3. Leia: .aioboss/GITHUB_TEMPLATE/agents/*.agent.md
4. Escanear repositório (README.md, package.json, src/)
5. Criar .aioboss/CONTEXT.md mapeando estado atual
6. Indexar chunks em .aioboss/chunks/
7. Confirme quando pronto: "✅ FIREMAN ENGAGED"

Princípios: DRY, KISS, SSOT
Retórica: Ethos, Pathos, Logos
"""

Copilot (agindo como Context Engineer):
> read_file: .aioboss/agent-architecture.md
> read_file: .aioboss/copilot-instructions.md
> read_file: README.md, package.json
> grep_search: "export", "import", "function", "const"
> find_files: "*.ts", "*.tsx", "*.js", "*.jsx"

[ANÁLISE DETALHADA DO CÓDIGO]

Copilot output:
"""
🚨 FIREMAN ACTIVATED

✅ Repositório mapeado:
   - Tecnologia: React + TypeScript + Tailwind
   - Arquivos: 156
   - Módulos: 12
   - Tests: 23 (coverage: 45%)
   - Last commit: 3 dias atrás

📊 Estado atual documentado:
   - Componentes: Editor, Dashboard, API Routes
   - State Management: Zustand
   - Database: Supabase PostgreSQL
   - Auth: JWT sessions

📝 CONTEXT.md criado em .aioboss/CONTEXT.md
📍 5 chunks indexados em .aioboss/chunks/
   - c1-arch-overview.md
   - c2-auth-flow.md
   - c3-db-schema.md
   - c4-components-structure.md
   - c5-state-management.md

🎯 Próximas ações recomendadas:
   1. Aumentar cobertura de testes (45% → 80%)
   2. Documentar fluxos críticos (auth, payments)
   3. Refatorar componentes monolíticos

Aguardando instrução. Qual é seu próximo move?
"""
```

### FASE 3: Operação (Você + Copilot, Iterativo)

```
Você:
"Preciso implementar pagamento com Stripe. Qual é o plano?"

Copilot (assumindo role de Task Planner):
"""
📋 Plano de Execução (baseado em CONTEXT.md):

1. [Context Engineer] Mapear estado de payments
   - Verificar se há integração parcial
   - Atualizar CONTEXT.md

2. [Dev Agent] Implementar Stripe SDK
   - yarn add @stripe/react-stripe-js
   - Criar src/lib/stripe-client.ts
   - Implementar checkout flow

3. [Dev Agent] Criar testes
   - src/__tests__/stripe-integration.test.ts
   - Coverage > 80%

4. [Dev Agent] Sincronizar CONTEXT.md
   - Adicionar à seção "Payments Architecture"
   - Atualizar chunks/

Quer que eu comece?
"""

Você: "Sim"

[Sistema procede como FASE 3 do documento original]
```

---

## 📋 O QUE MUDA AGORA: Decisões Finalizadas

### ✅ Pergunta 1: Integração com VSCode

**Decisão: HYBRID**

```
├─ VSCode native: cria .github/copilot-instructions.md genérico (auto)
├─ AIOBoss: você digita prompt "ACTIVATE FIREMAN MODE"
└─ Resultado: 2-step, zero dependência de VSCode detectar nada
```

**Por quê?**
- VSCode não precisa "saber" que AIOBoss existe
- Você tem controle 100% (quando ativa, como ativa)
- Funciona em qualquer plataforma (Cursor, GitHub Web, Claude, etc)
- Zero lock-in com VSCode

---

### ✅ Pergunta 2: Onde Vive o "Master Prompt"

**Decisão: OPÇÃO 3 (Ambos, com integração)**

```
.github/copilot-instructions.md
└─ Instruções gerais do projeto
   └─ "Para ativar sistema agentico avançado, veja .aioboss/copilot-instructions.md"

.aioboss/copilot-instructions.md
└─ MASTER PROMPT (SSOT operacional)
   ├─ Agent architecture
   ├─ Role definitions
   ├─ CONTEXT.md protocol
   ├─ Bootstrap flow
   └─ Integration patterns
```

**Por quê?**
- `.github/` segue convenção VSCode nativa
- `.aioboss/` é seu espaço de propriedade 100%
- Cross-referencing = Zero duplicação
- Suporta descentralização (você governa AIOBoss, VSCode governa VSCode)

---

### ✅ Pergunta 3: O Bootstrap Prompt

**Decisão: OPÇÃO 2 (Enxuto, autocontido no AIOBoss)**

```
bootstrap-prompt.md (10 linhas)
└─ Digitar no Copilot:
   "ACTIVATE FIREMAN MODE. Carregue dados agênticos do #aioboss"

Copilot internamente:
├─ Lê .aioboss/agent-architecture.md
├─ Lê .aioboss/copilot-instructions.md
├─ Lê .aioboss/GITHUB_TEMPLATE/agents/*.agent.md
└─ Executa bootstrap automático
```

**Por quê?**
- Inteligência está NO AIOBOSS (não distribuída)
- Prompt é apenas "trigger"
- Solo founder digita 1 linha, magic happens
- Agnóstico de idioma (funciona em PT-BR, EN, ES, FR)

---

## 🔥 O ALGORITMO DE INTEGRAÇÃO (Pseudo-código)

### Migration Pattern: Inner Join Lógico

```yaml
Algoritmo: Migracao_Template_AutoContext

Entrada:
  - Template_Original: .aioboss/ (estrutura vazia)
  - Repositorio_Destino: seu-projeto/ (caos existente)
  - Operacao: INNER_JOIN (intersecção lógica)

Processo:
  1. PARA CADA Arquivo em Repositorio_Destino:
       - BUSCAR correspondência em Template_Original
       - SE encontrado:
           MAPEAR contexto (arquivo → chunk)
           ADICIONAR a CONTEXT.md
       - SENAO:
           MARCAR como "new context"
           CRIAR novo chunk

  2. PARA CADA Instrucao em Template_Original:
       - VALIDAR se tem equivalente no Repositorio_Destino
       - SE nao encontrado:
           AVISO: "Context ausente - será criado vazio"
       - SE encontrado:
           LINKEAR + CRIAR referência cruzada

  3. RETORNAR:
       - CONTEXT.md preenchido (estado atual)
       - chunks/ indexados (RAG pronto)
       - agent-architecture.md carregado (agentes prontos)

Resultado:
  ✅ Memória sincronizada com realidade
  ✅ Agentes entendem seu código
  ✅ Zero alucinações sobre estrutura
```

---

## 📐 ESTRUTURA FINAL DO AIOBOSS

### Arquivo 1: `.aioboss/agent-architecture.md`

```markdown
# AIOBoss Agent Architecture

## System Overview
Este é um sistema agentico descentralizado baseado em Context Engineering.

## Agentes Core (4)

### 1. Context Engineer
- **Responsabilidade:** Mapear, indexar, sincronizar CONTEXT.md
- **Acionado quando:** "map project", "update context"
- **Output:** CONTEXT.md + chunks indexados

### 2. Task Planner
- **Responsabilidade:** Quebrar requisitos em sub-tasks
- **Acionado quando:** "como implementar X?"
- **Output:** Plano estruturado + checklist

### 3. Dev Agent
- **Responsabilidade:** Implementar código, testes, PRs
- **Acionado quando:** Task Planner → Dev Agent (chain)
- **Output:** Código + testes + diffs para aprovação

### 4. Head-of-Office
- **Responsabilidade:** Governança, aprovações críticas
- **Acionado quando:** Antes de merge em main/prod
- **Output:** Aprovação + escalação se necessário

## Restrições Globais
- ✅ Sempre check CONTEXT.md antes de agir
- ❌ Nunca push/merge sem aprovação humana
- ❌ Nunca exponha secrets/credenciais
- ✅ Sempre prepare diffs para revisão

## Sucesso = Quando
- semantic_search retorna contexto em < 250ms
- 100% de mudanças documentadas
- 100% de mudanças críticas com aprovação
- Zero inconsistências (CONTEXT.md ↔ código)
```

### Arquivo 2: `.aioboss/copilot-instructions.md`

```markdown
# AIOBoss Copilot Instructions (MASTER PROMPT)

**Este é seu SSOT operacional. Todos os agentes consultam isto primeiro.**

## Você é um Sistema Agentico

### Descoberta Inicial
1. Leia: .aioboss/agent-architecture.md (você tem 4 roles)
2. Leia: .aioboss/CONTEXT.md (estado atual do projeto)
3. Leia: .aioboss/chunks/ (índice para RAG)
4. Consulte: seu código em src/

### Seus Roles (Assumption Pattern)

Dependendo do request do usuário, assuma o role apropriado:

**Request contém "map", "analyze", "understand"?**
→ Assuma role: Context Engineer

**Request contém "como", "plano", "plan", "steps"?**
→ Assuma role: Task Planner

**Request contém "implementar", "code", "test", "arquivo"?**
→ Assuma role: Dev Agent

**Request contém "aprove", "merge", "deploy", "critical"?**
→ Assuma role: Head-of-Office

### Princípios Operacionais

```
DRY   = Não repita informações (tudo está em CONTEXT.md)
KISS  = Mantenha simples (prefira 3 passos a 10)
SSOT  = CONTEXT.md é a verdade (não alucinhe)
Ethos = Seja credível no seu domínio (conheça o código)
Pathos = Entenda o usuário (respeite restrições dele)
Logos = Explique raciocínio (faça planos estruturados)
```

### Seu Comportamento

- ✅ Sempre check CONTEXT.md primeiro
- ✅ Se falta contexto, ask ou map (Context Engineer)
- ✅ Prepare apply_patch diffs (nunca auto-apply)
- ✅ Escale decisões críticas (CI/CD, API pública, deploy)
- ❌ Nunca push/merge sem aprovação explícita
- ❌ Nunca exponha credenciais, secrets, API keys
- ❌ Nunca modifique CI/CD sem aprovação

### Sucesso Criteria

- ✅ semantic_search encontra contexto em < 250ms
- ✅ Todas mudanças estão documentadas antes de PR
- ✅ CONTEXT.md nunca fica desatualizado
- ✅ Agentes NÃO alucinam (usam memória, não imaginação)

## Próximo: Aguarde instrução do usuário
```

### Arquivo 3: `.aioboss/CONTEXT.md` (Template)

```markdown
# CONTEXT.md

**Auto-updated by:** Context Engineer  
**Last scan:** [AUTO]  
**Status:** ✅ Synchronized

## Project Identity

| Chave              | Valor                        |
| ------------------ | ---------------------------- |
| Nome               | [AUTO]                       |
| Repositório        | [AUTO]                       |
| Stack              | [AUTO]                       |
| Fase               | Prototype / MVP / Production |
| Última modificação | [AUTO]                       |

## Current State

### Codebase Overview
- **Total Files:** [AUTO]
- **Módulos:** [AUTO]
- **Tests:** [AUTO] (coverage: [AUTO]%)
- **Último commit:** [AUTO]
- **Branch ativa:** [AUTO]

### Architecture Summary
[AUTO-GENERATED from code structure]

### Critical Issues
- [Mapeado automaticamente]

### Next Steps
- [Recomendações do Context Engineer]

## RAG Chunks Index

| ID  | Summary | Source | Keywords |
| --- | ------- | ------ | -------- |
| c1  | [AUTO]  | [AUTO] | [AUTO]   |
| c2  | [AUTO]  | [AUTO] | [AUTO]   |

---

**Próxima atualização:** Quando Context Engineer for acionado (ou a cada 24h)
```

---

## 📦 TIER 1 ARTIFACTS (O Que Criar Agora)

### ✅ Artefato 1: `bootstrap-prompt.md`

```markdown
# BOOTSTRAP PROMPT (Copy-Paste)

Digitar isto no Copilot quando quiser ativar AIOBoss:

"""
🚨 ACTIVATE FIREMAN MODE

Carregue os dados agênticos do #aioboss.

Siga:
1. Leia: .aioboss/agent-architecture.md
2. Leia: .aioboss/copilot-instructions.md (MASTER)
3. Leia: .aioboss/GITHUB_TEMPLATE/agents/*.agent.md
4. Escanear repositório (README, package.json, src/)
5. Criar .aioboss/CONTEXT.md com estado atual
6. Indexar chunks em .aioboss/chunks/
7. Confirme quando pronto: "✅ FIREMAN ENGAGED"

Princípios: DRY, KISS, SSOT
Retórica: Ethos, Pathos, Logos
"""
```

### ✅ Artefato 2: `context-engineer.agent.md` (COMPRESSED)

```markdown
# Context Engineer Agent Definition

**Role:** Engenheiro de Contexto  
**Nível:** Sênior  
**Owner:** SSOT, RAG, CONTEXT.md

## Seu Papel
Capturar, indexar, sincronizar conhecimento do projeto.

## Acionado Quando
- User: "map project", "update context", "what's architecture?"
- Outro agente precisa de refresh
- semantic_search retorna baixa cobertura

## Workflow (Sempre Nessa Ordem)

### 1. Descoberta
- read_file: README.md, package.json, src/ (30 arquivos principais)
- grep_search: palavras-chave (auth, db, api, component)
- Identificar gaps (o que falta doc? o que está desatualizado?)

### 2. Plano
- Produzir Markdown com passos atômicos
- Listar tools necessárias
- Listar testes/validações

### 3. Chunking
- Dividir contexto em blocos (ID + summary + source + keywords)
- Salvar em .aioboss/chunks/ (markdown)

### 4. Diffs
- Se edita arquivos, usar apply_patch
- Nunca aplicar sem aprovação
- Incluir contexto antes/depois

### 5. Output
```json
{
  "objective": "Map current auth system",
  "chunks": [
    {"id": "c2-auth", "summary": "JWT + sessions", "source": "src/auth/", "keywords": ["auth", "jwt"]}
  ],
  "plan": [
    {"step": 1, "description": "Scan auth files", "tool": "read_file + grep_search"}
  ],
  "tests": ["cd . && yarn test src/auth --coverage"],
  "prChecklist": ["typecheck", "lint", "tests"]
}
```

### 6. Escalation
- Se altera API pública, CI/CD, deploy → Head-of-Office

## Restrições
- ❌ Não faça push/merge
- ❌ Não exponha secrets
- ❌ Não aplique patches sem aprovação
- ❌ Não modifique CI/CD

## Sucesso
- ✅ semantic_search < 250ms
- ✅ 100% documentado
- ✅ Chunks indexados
- ✅ CONTEXT.md ↔ código sincronizado
```

### ✅ Artefato 3: `example-fireman-activation.md`

```markdown
# Exemplo: Activar Fireman Mode

## Cenário: Solo Founder em Caos

Você tem:
- Projeto em desenvolvimento há 45 dias
- 200+ arquivos
- Perdeu o mapa mental
- Copilot não entende a arquitetura
- Precisa de resgate AGORA

## Passo 1: Setup (5 min)

```bash
cd seu-projeto
cp -r ~/aioboss/.aioboss ./.aioboss
code .
```

## Passo 2: Ativar Fireman (30 min)

Digitar no Copilot:

```
🚨 ACTIVATE FIREMAN MODE

Carregue os dados agênticos do #aioboss.

Siga:
1. Leia: .aioboss/agent-architecture.md
2. Leia: .aioboss/copilot-instructions.md
3. Leia: .aioboss/GITHUB_TEMPLATE/agents/*.agent.md
4. Escanear repositório (README, package.json, src/)
5. Criar .aioboss/CONTEXT.md com estado atual
6. Indexar chunks em .aioboss/chunks/
7. Confirme quando pronto: "✅ FIREMAN ENGAGED"
```

## Passo 3: Context Engineer Executa

Copilot mapa seu projeto:

```
✅ FIREMAN ACTIVATED

📊 Repositório mapeado:
   - React + TypeScript + Tailwind
   - 156 arquivos, 12 módulos
   - 23 testes (coverage: 45%)

📝 CONTEXT.md criado
📍 5 chunks indexados

🎯 Próximas ações:
   1. Aumentar test coverage (45% → 80%)
   2. Documentar fluxos críticos
   3. Refatorar componentes monolíticos
```

## Passo 4: Você Está Rescatado

Agora você pode:

```
Você: "Preciso implementar pagamento. Qual é o plano?"

Task Planner responde:
📋 Plano estruturado:
1. Context Engineer → mapeia estado de payments
2. Dev Agent → implementa Stripe
3. Dev Agent → cria testes
4. Context Engineer → sincroniza CONTEXT.md

Quer que eu comece?
```

## Resultado: 30 Minutos de Fireman

```
✅ Seu projeto mapeado
✅ Você entende sua arquitetura novamente
✅ Copilot tem memória (CONTEXT.md)
✅ Agentes trabalham em harmonia
✅ Pronto para escalar ou contratar com contexto claro
```
```

---

## 🎯 METRICS DE SUCESSO

Você saberá que **Fireman** está funcionando quando:

```
✅ Novo dev clona → entende arquitetura em < 5 min
✅ Agentes NÃO alucinam (usam CONTEXT.md)
✅ Feature inteira delegada sem supervisão constante
✅ CONTEXT.md nunca fica desatualizado
✅ Solo founder tem "virtual dev team"
✅ Zero lock-in (é markdown + prompts)
✅ Histórico completo (auditável em git)
```

---

## 📦 STATUS FINAL

### ✅ Decisões Fechadas

| Pergunta               | Resposta                     |
| ---------------------- | ---------------------------- |
| VSCode Integration     | HYBRID (auto + manual)       |
| Master Prompt Location | Ambos (.github/ + .aioboss/) |
| Bootstrap Prompt       | Enxuto (1 liner + automagic) |
| **Codinome**           | **Fireman / AIOBoss**        |

### ✅ Tier 1 Artifacts (Prontos para Criar)

- [ ] `bootstrap-prompt.md` — Trigger para Fireman
- [ ] `context-engineer.agent.md` — Role definition
- [ ] `agent-architecture.md` — System overview
- [ ] `copilot-instructions.md` — Master prompt
- [ ] `CONTEXT.md` — Template
- [ ] `example-fireman-activation.md` — Caso real

---

## 🚀 PRÓXIMO PASSO

**Você aprova este racional atualizado?**

Se SIM → Criaremos os 6 arquivos Tier 1 em 30 min. AIOBoss/Fireman estará vivo.

Se NÃO → Qual ajuste precisa?

---

**Versão:** 1.1.0 (Fireman Integration)  
**Status:** Ready for Implementation  
**Data:** 2024-12-07 21:29 UTC-3  
**Por:** Context Engineering Framework
