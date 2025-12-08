# EXEMPLO: ACTIVATE AIOBoss MODE

**Cenário Real:** Solo dev em caos tentando resgatar um projeto

**ID:** 071225-220700  
**Status:** Exemplo Completo (você pode replicar este workflow)

---

## 📍 SITUAÇÃO INICIAL

Você tem:

```text
- Projeto em desenvolvimento há 60 dias
- 250+ arquivos em src/, api/, db/
- Código cresceu desordenado (sem arquitetura inicial)
- 3 tentativas de refactor (todas fracassaram)
- Você perdeu o mapa mental de como funciona
- Copilot/Claude alucinam quando você pede "explica a arquitetura"
- Deadline em 3 semanas
- Budget: R$0 (você é solo)
```

**Problema:** Você não consegue nem iniciar feature nova porque não sabe como o código encaixa.

---

## 🚀 PASSO 1: SETUP (5 MINUTOS)

### 1.1 Clonar seu repositório

```bash
cd ~/projects
git clone https://github.com/seu-usuario/seu-projeto
cd seu-projeto
code .
```

### 1.2 Copiar estrutura AIOBoss

```bash
# Opção A: Se você tem o aioboss clonado localmente
cp -r ~/aioboss/aioboss ./aioboss

# Opção B: Se você quer download do GitHub
mkdir -p aioboss
curl -L https://github.com/aiob3/aioboss/archive/main.zip -o /tmp/aioboss.zip
unzip /tmp/aioboss.zip -d /tmp
cp -r /tmp/aioboss-main/aioboss/* ./aioboss/
```

### 1.3 Verificar estrutura

```bash
ls -la aioboss/
# Deve aparecer:
# - agent-architecture.md
# - copilot-instructions.md
# - GITHUB_TEMPLATE/
# - CONTEXT.md (template)
# - chunks/ (vazio)
```

---

## 🔥 PASSO 2: ATIVAR AIOBoss (30 MINUTOS)

### 2.1 Abrir Copilot Chat

Em VSCode:

- `Cmd+Shift+P` (macOS) ou `Ctrl+Shift+P` (Windows)
- Digitar: "Copilot: Open Chat"
- Ou: `Ctrl+L` (atalho direto)

### 2.2 Digitar o Bootstrap Prompt

```text
🚨 ACTIVATE AIOBoss MODE

Carregue os dados agênticos do #aioboss.

Siga:
1. Leia: aioboss/agent-architecture.md
2. Leia: aioboss/copilot-instructions.md (MASTER)
3. Leia: aioboss/GITHUB_TEMPLATE/agents/*.agent.md
4. Escanear repositório (README, package.json, src/, main code files)
5. Gerar aioboss/CONTEXT.md com estado atual
6. Indexar chunks em aioboss/chunks/
7. Confirme quando pronto: "✅ AIOBoss ENGAGED"

Princípios: DRY, KISS, SSOT
Retórica: Ethos, Pathos, Logos
```

### 2.3 Copilot Executa (Assistir)

Copilot vai:

```text
✅ FASE 1: READ (2-3 min)
> read_file: aioboss/agent-architecture.md
> read_file: aioboss/copilot-instructions.md
> read_file: aioboss/GITHUB_TEMPLATE/agents/context-engineer.agent.md
> read_file: aioboss/GITHUB_TEMPLATE/agents/task-planner.agent.md
> read_file: aioboss/GITHUB_TEMPLATE/agents/dev-agent.agent.md
> read_file: aioboss/GITHUB_TEMPLATE/agents/head-of-office.agent.md

[Copilot responde]
✅ Carregadas definições de 4 agentes
✅ Master prompt em memória
✅ Arquitetura compreendida

---

✅ FASE 2: SCAN (5-10 min)
> read_file: README.md
> read_file: package.json
> find_files: src/**/*.ts, src/**/*.tsx, src/**/*.js, api/**/*.ts
> find_files: __tests__/**/*
> [Analisa estrutura]

[Copilot responde com resumo:]
✅ Repositório mapeado:

📊 ESTATÍSTICAS:
   - Total files: 234
   - Linhas de código: 45,230
   - Módulos identificados: 18
   - Testes: 42 files (coverage: 52%)
   - Último commit: 2 dias atrás
   - Branch: main

🏗️ ARQUITETURA DETECTADA:
   Frontend: React 18 + TypeScript + Tailwind
   Backend: Express.js + TypeScript
   Database: PostgreSQL (Prisma ORM)
   Auth: JWT sessions
   Hosting: Vercel (frontend) + Railway (backend)

📁 MÓDULOS PRINCIPAIS:
   ├─ src/components/ (React components, 45 files)
   ├─ src/pages/ (Next.js pages, 12 files)
   ├─ src/hooks/ (Custom hooks, 8 files)
   ├─ src/api/ (API routes, 18 files)
   ├─ src/db/ (Database queries, 15 files)
   ├─ src/auth/ (Auth logic, 7 files)
   ├─ src/lib/ (Utilities, 23 files)
   └─ src/types/ (TypeScript types, 12 files)

⚠️ GAPS & ISSUES DETECTADOS:
   - Falta documentação em 8 componentes críticos
   - Duplicação de código em auth (2 implementações)
   - Test coverage abaixo do target (52% vs 80%)
   - Componentes monolíticos em pages/ (refactor necessário)

---

✅ FASE 3: GENERATE CONTEXT.MD (3-5 min)

Criando aioboss/CONTEXT.md com:
   - Project identity (nome, repo, tech stack)
   - Codebase snapshot (stats, estrutura)
   - Architecture overview (diagram ASCII)
   - Current state (o que funciona, bloqueadores)
   - Critical issues (3 issues altos)
   - Next milestones (onde ir)
   - Segurança & compliance (checklist)

[Escreve CONTEXT.md no disco]

---

✅ FASE 4: INDEX CHUNKS (5 min)

Criando aioboss/chunks/:

   > create_file: aioboss/chunks/c1-arch-overview.md
     Sumário: Visão geral de alta nível da arquitetura
     Keywords: [arch, design, components, modules, dependencies]

   > create_file: aioboss/chunks/c2-auth-system.md
     Sumário: Como JWT sessions e autenticação funcionam
     Keywords: [auth, jwt, sessions, login, logout]

   > create_file: aioboss/chunks/c3-db-schema.md
     Sumário: Database schema (tabelas, relacionamentos, migrations)
     Keywords: [database, schema, prisma, migrations, tables]

   > create_file: aioboss/chunks/c4-components-structure.md
     Sumário: React components (organização, patterns, shared)
     Keywords: [components, react, ui, patterns, reusable]

   > create_file: aioboss/chunks/c5-api-routes.md
     Sumário: API endpoints (métodos, autenticação, validação)
     Keywords: [api, routes, rest, endpoints, validation]

[5 chunks criados e indexados para busca semântica]

---

✅ AIOBoss ENGAGED

Sistema agentico ativo. Pronto para receber tarefas.

Estado do projeto mapeado e documentado em aioboss/CONTEXT.md
Memória indexada em aioboss/chunks/
Agentes prontos: Context Engineer, Task Planner, Dev Agent, Head-of-Office

Próxima ação: Qual é seu requisito?
```

---

## ✅ PASSO 3: VOCÊ FOI RESCATADO (5 MINUTOS)

Agora seu projeto está **governado e estruturado**.

### O Que Mudou?

```text
ANTES:
❌ Você não sabe a arquitetura
❌ Copilot alucina (sem contexto)
❌ Features novas = risco
❌ Code review = impossível
❌ Documentação = desatualizada

DEPOIS:
✅ aioboss/CONTEXT.md = VERDADE (atualizado)
✅ aioboss/chunks/ = RAG index (busca semântica rápida)
✅ Copilot/Claude tem MEMÓRIA (não alucina)
✅ Features novas = planejadas (Task Planner)
✅ Implementação = estruturada (Dev Agent)
✅ Approval = automático (Head-of-Office)
```

---

## 🎯 PASSO 4: USE OS AGENTES (AGORA)

### Exemplo 1: "Qual é o estado do meu projeto?"

```text
Você: Qual é o estado atual do meu projeto?

Copilot (Context Engineer mode):
✅ CONTEXT.md atualizado em: 2024-12-07 23:45

📊 RESUMO EXECUTIVO:
   - Fase: MVP (pronto para beta)
   - Health: 🟡 Mediana
   - Coverage: 52% (alvo: 80%)
   - Open issues: 7 (2 críticos)
   - Bloqueadores: Auth refactor, test coverage

🎯 PRÓXIMOS PASSOS:
   1. Aumentar test coverage (52% → 80%)
   2. Refactor auth duplicado
   3. Documentar 8 componentes críticos
   4. Feature nova: pagamento (Stripe)

Qual desses você quer atacar primeiro?
```

### Exemplo 2: "Preciso implementar pagamento com Stripe. Qual é o plano?"

```text
Você: Preciso implementar pagamento com Stripe em 5 dias. Qual é o plano?

Copilot (Task Planner mode):
📋 PLANO: Stripe Payment Integration

Duração estimada: 40 horas (5 dias @ 8h/dia)
Risco: Médio (envolve dados sensíveis)

FASE 1: SETUP (Day 1 - 8h)
  Task 1.1: Setup Stripe account + API keys
    - Responsável: Você (manual)
    - Tempo: 1h
    - Dependências: Nenhuma
    - Output: Stripe account com test keys

  Task 1.2: Instalar @stripe/react-stripe-js + @stripe/stripe-js
    - Responsável: Dev Agent
    - Tempo: 30min
    - Dependências: Task 1.1
    - Output: yarn.lock atualizado

  Task 1.3: Criar Stripe service (backend)
    - Responsável: Dev Agent
    - Tempo: 3h
    - Dependências: Task 1.1
    - Output: src/lib/stripe-service.ts

  Task 1.4: Criar checkout route (/api/checkout)
    - Responsável: Dev Agent
    - Tempo: 3.5h
    - Dependências: Task 1.3
    - Output: pages/api/checkout.ts

FASE 2: FRONTEND (Day 2-3 - 16h)
  Task 2.1: Criar CheckoutForm component
    - Responsável: Dev Agent
    - Tempo: 4h
    - Dependências: Task 1.3
    - Output: src/components/CheckoutForm.tsx

  Task 2.2: Integrar em pages/pricing
    - Responsável: Dev Agent
    - Tempo: 2h
    - Dependências: Task 2.1
    - Output: pages/pricing.tsx (atualizado)

  Task 2.3: Testes e validação
    - Responsável: Dev Agent
    - Tempo: 8h
    - Dependências: Task 2.1, 2.2
    - Output: __tests__/checkout.test.ts (>80% coverage)

  Task 2.4: Tratamento de erros
    - Responsável: Dev Agent
    - Tempo: 2h
    - Dependências: Task 2.1
    - Output: Error handling + retry logic

FASE 3: BACKEND (Day 3-4 - 12h)
  Task 3.1: Database schema (payments table)
    - Responsável: Dev Agent
    - Tempo: 1h
    - Dependências: Nenhuma
    - Output: prisma/schema.prisma (migrations)

  Task 3.2: Webhook handler (/api/webhook)
    - Responsável: Dev Agent
    - Tempo: 4h
    - Dependências: Task 3.1, 1.3
    - Output: pages/api/webhook.ts

  Task 3.3: Validação e segurança
    - Responsável: Dev Agent
    - Tempo: 4h
    - Dependências: Task 3.2
    - Output: src/lib/stripe-validation.ts

  Task 3.4: Testes
    - Responsável: Dev Agent
    - Tempo: 3h
    - Dependências: Task 3.2, 3.3
    - Output: __tests__/payments.test.ts

FASE 4: DOCS & DEPLOY (Day 5 - 4h)
  Task 4.1: Documentação
    - Responsável: Context Engineer
    - Tempo: 1h
    - Dependências: Todas as tasks anteriores
    - Output: docs/STRIPE_SETUP.md

  Task 4.2: Update CONTEXT.md
    - Responsável: Context Engineer
    - Tempo: 1h
    - Dependências: Todas as tasks anteriores
    - Output: aioboss/CONTEXT.md atualizado

  Task 4.3: Deploy para staging
    - Responsável: Dev Agent + Head-of-Office
    - Tempo: 1h
    - Dependências: Todas as tasks anteriores
    - Output: Staging deployment + test

  Task 4.4: E2E test + approval
    - Responsável: Você + Head-of-Office
    - Tempo: 1h
    - Dependências: Task 4.3
    - Output: Aprovado para prod

🚨 RISCOS IDENTIFICADOS:
   - Stripe API complexity (mitigação: documentação detalhada)
   - PCI compliance (mitigação: usar Stripe Elements, não capturar cards)
   - Test coverage crítico (mitigação: >90% em payments)

❓ APROVADO PARA COMEÇAR?
   Y/N: Sim, comece com Task 1.1
```

### Exemplo 3: "Dev Agent, implementa Task 1.2 (instalar Stripe SDK)"

```text
Você: Dev Agent, implementa Task 1.2 (instalar Stripe SDK)

Copilot (Dev Agent mode):
📌 TASK 1.2: Instalar Stripe SDK

Dependências: Task 1.1 (Stripe account) ✅ Já feito
Tempo estimado: 30min
Output esperado: yarn.lock atualizado + import verificado

---

🔍 PHASE 1: ANÁLISE

Lendo package.json atual...
✅ Usando Node 18.17.1
✅ Usando yarn 3.6.0
✅ React 18.2.0 + TypeScript 5.1.6

Plano:
1. yarn add @stripe/react-stripe-js @stripe/stripe-js
2. Verificar tipos (TypeScript)
3. Test import
4. Update CONTEXT.md (dependências)

---

💻 PHASE 2: IMPLEMENTAÇÃO

Preparando diffs:

--- /dev/null
+++ b/src/lib/stripe-client.ts
@@ -0,0 +1,18 @@
+import { loadStripe } from '@stripe/stripe-js';
+
+/**
+ * Initialize Stripe client
+ * Public key from env (safe to expose)
+ */
+export const stripePromise = loadStripe(
+  process.env.NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY!,
+  {
+    apiVersion: '2023-10-16',
+  }
+);

--- a/package.json
+++ b/package.json
@@ -15,6 +15,8 @@
   "dependencies": {
+    "@stripe/react-stripe-js": "^2.4.0",
+    "@stripe/stripe-js": "^2.4.0",
     "react": "^18.2.0",

---

✅ PHASE 3: VALIDAÇÃO

✅ TypeScript check (tsc --noEmit)
✅ ESLint check (eslint src/lib/stripe-client.ts)
✅ Yarn.lock updated (yarn install)
✅ Import teste (TypeScript compilation OK)

---

📝 PHASE 4: OUTPUT

Diffs prontos para aplicar:
1. yarn add @stripe/react-stripe-js @stripe/stripe-js
2. Novo arquivo: src/lib/stripe-client.ts
3. Atualizado: yarn.lock

✅ Definition of Done:
   ✅ Código passa ESLint
   ✅ TypeScript strict mode (0 errors)
   ✅ Imports funcionam
   ✅ Documentação inline
   ✅ CONTEXT.md atualizado (novas dependências)

Próxima: Task 1.3 (Stripe service) ou aguardar?
```

### Exemplo 4: "Head-of-Office, aprova?"

```text
Você: Head-of-Office, aprova antes de merge?

Copilot (Head-of-Office mode):
🔍 REVIEW: Task 1.2 Completion (Stripe SDK Install)

---

CHECKLIST DE APROVAÇÃO:

✅ Code Quality Gates?
   ✅ ESLint: passing
   ✅ TypeScript strict: 0 errors
   ✅ No security issues detected

✅ Definition of Done?
   ✅ Código completo
   ✅ Testes presentes
   ✅ Documentação atualizada
   ✅ CONTEXT.md sincronizado

✅ Risk Assessment?
   ✅ Baixo risco (apenas adicionar nova dependência)
   ✅ Stripe é library confiável (widely used)
   ✅ Sem breaking changes em dependências existentes

✅ Impact Analysis?
   ✅ Impacto: + 2 dependências, + 18KB bundle
   ✅ Performance: neglegível
   ✅ Compatibilidade: ✅ todas as versões OK

---

✅ APROVADO PARA MERGE

Task 1.2 está pronto.

Próximas ações:
1. yarn add (já feito localmente)
2. git commit -m "feat: add stripe sdk (Task 1.2)"
3. git push → Abre PR
4. Merge para main

🎯 Depois: Avance para Task 1.3 ou aguarde confirmation?
```

---

## 🎬 RESULTADO FINAL (Fim do Dia 1)

```text
ANTES (Início do dia):
❌ Você estava em caos
❌ 60 dias de código sem estrutura
❌ Copilot inutilizável
❌ Não sabia por onde começar

DEPOIS (Fim do dia):
✅ Projeto mapeado (aioboss/CONTEXT.md)
✅ Memória indexada (aioboss/chunks/ com RAG)
✅ Plano claro (5 dias, 4 fases, 15 tasks)
✅ Task 1.2 completa + aprovada
✅ Agentes funcionando (Context Eng, Task Planner, Dev, Head-of-Office)
✅ Pronto para escalar (99% de confiança)

TIMELINE:
- Setup: 5min
- ACTIVATE AIOBoss: 30min
- Leverage agentes: 25min
- TOTAL: 1 hora

VALUE DELIVERED:
- Recuperou projeto do caos
- Estrutura clara
- Memória persistente
- Agentes sincronizados
- Pronto para 3 semanas até deadline
```

---

## 💡 TAKEAWAYS

### O Que Você Aprendeu

1. **ACTIVATE AIOBoss MODE** = seu atalho para resgate
2. **Context Engineering** = memória persistente (não dependa só de prompt)
3. **Multi-agent orchestration** = delegue tarefas a agentes, você aprova
4. **SSOT** = nunca perca a arquitetura novamente
5. **DRY/KISS/SSOT** = princípios simples, resultados poderosos

### Próximas Vezes

- Novo projeto? Copie aioboss/ no dia 1
- Projeto em caos? ACTIVATE AIOBoss MODE
- Quer rescan? RESCAN AIOBoss
- Dúvida sobre arquitetura? Verifique CONTEXT.md

### Suporte

- CONTEXT.md = SSOT (verdade)
- chunks/ = busca rápida (RAG)
- copilot-instructions.md = regras dos agentes
- agent-architecture.md = governança

---

**ID:** 071225-220700  
**Status:** Exemplo Funcional Completo  
**Versão:** 1.0.0  
**Tempo Total de Setup:** ~1 hora  
**ROI:** Você salva seu projeto do caos + prepara para escala
