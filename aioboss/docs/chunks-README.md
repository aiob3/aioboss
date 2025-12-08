# chunks/ - RAG INDEX PARA BUSCA SEMÂNTICA

**Diretório:** `aioboss/chunks/`  
**Propósito:** Índice distribuído para RAG (Retrieval Augmented Generation)  
**Owner:** Context Engineer (auto-maintained)  
**Atualização:** Quando CONTEXT.md é atualizado

---

## O Que São Chunks?

**Chunks** são **fragmentos de documentação** que dividem o conhecimento do seu projeto em pedaços menores, otimizados para busca semântica.

Quando você digita:

```text
"Como funciona autenticação no meu projeto?"
```

Copilot não lê toda a documentação. Ele faz **busca semântica** nos chunks:

```text

Query: "autenticação"
      ↓
Busca em: c2-auth-system.md
          keywords: [auth, jwt, login, logout, sessions]
      ↓
Retorna: Conteúdo relevante em < 250ms
      ↓
Copilot: "Baseado em c2-auth-system.md, aqui está como funciona..."
```

---

## Estrutura de um Chunk

Cada arquivo `.md` em `chunks/` segue este padrão:

```markdown
# c{N}-{IDENTIFICADOR}

**ID:** c{N}  
**Resumo:** Uma linha descrevendo o conteúdo  
**Últimamente atualizado:** [AUTO]  
**Keywords:** [kw1, kw2, kw3, ...]  
**Relacionados:** c{N-1}, c{N+1}  

---

## Descrição (Conteúdo Real)

[Seu conteúdo documentado aqui, tipicamente 500-1500 palavras]

---

## Quando Usar

Use este chunk quando:
- Você quer entender [tópico]
- Você está implementando [feature]
- Você precisa debugar [problema]

## Quick Reference

[Código, diagramas, exemplos rápidos]

---

**Status:** Current  
**Próxima revisão:** [Data]
```

---

## Convenção de Nomes

| Padrão           | Exemplo                      | Propósito                    |
| ---------------- | ---------------------------- | ---------------------------- |
| `c1-arch-*`      | `c1-arch-overview.md`        | Arquitetura de alto nível    |
| `c2-auth-*`      | `c2-auth-system.md`          | Autenticação e segurança     |
| `c3-db-*`        | `c3-db-schema.md`            | Database e persistência      |
| `c4-component-*` | `c4-components-structure.md` | Componentes e UI             |
| `c5-api-*`       | `c5-api-routes.md`           | API e integração             |
| `c6-deploy-*`    | `c6-deploy-pipeline.md`      | DevOps e deploy              |
| `c7-{domain}-*`  | Customizado                  | Adicione conforme necessário |

**Padrão:** `c{SEQUÊNCIA}-{DOMÍNIO}-{DESCRIÇÃO}.md`

---

## Chunks Típicos Para Incluir

Quando Context Engineer roda, ele deve gerar **mínimo 5 chunks**:

### Tier 1 (Obrigatório)

```text
✅ c1-arch-overview.md
   Resumo: Arquitetura de alto nível (componentes, fluxos, integrações)
   Keywords: [arch, design, components, modules, flow, dependencies]
   
✅ c2-auth-system.md
   Resumo: Sistema de autenticação (como login, JWT, sessions)
   Keywords: [auth, authentication, jwt, sessions, login, logout, secure]
   
✅ c3-db-schema.md
   Resumo: Database schema (tabelas, relacionamentos, tipos)
   Keywords: [database, schema, tables, migrations, data model]
   
✅ c4-components-structure.md
   Resumo: Frontend structure (components, hooks, state management)
   Keywords: [components, frontend, react, structure, ui, hooks]
   
✅ c5-api-routes.md
   Resumo: API endpoints (métodos, validação, rate limiting)
   Keywords: [api, routes, rest, endpoints, validation, http]
```

### Tier 2 (Recomendado Se Aplicável)

```text
⭐ c6-deploy-pipeline.md
   Resumo: CI/CD e processo de deploy (staging, production)
   Keywords: [deploy, ci-cd, github actions, testing, releases]
   
⭐ c7-testing-strategy.md
   Resumo: Estratégia de testes (unit, integration, e2e)
   Keywords: [testing, tests, jest, coverage, quality, tdd]
   
⭐ c8-security-checklist.md
   Resumo: Segurança (secrets, encryption, compliance)
   Keywords: [security, encryption, secrets, compliance, gdpr, soc2]
   
⭐ c9-performance-optimization.md
   Resumo: Performance (caching, database optimization, frontend bundles)
   Keywords: [performance, optimization, caching, speed, bundle]
```

### Tier 3 (Domain-Specific)

```text
🔧 c10-payments-integration.md
   Se você tem: Stripe, Paddle, Square, etc.
   
🔧 c11-third-party-apis.md
   Se você tem integrações: SendGrid, Slack, etc.
   
🔧 c12-mobile-app.md
   Se você tem: React Native, Flutter, etc.
```

---

## Exemplo: Chunk Real

### Arquivo: `c2-auth-system.md`

```markdown
# c2-auth-system

**ID:** c2  
**Resumo:** Sistema de autenticação JWT com sessions persistentes  
**Último update:** 2024-12-07  
**Keywords:** [auth, jwt, sessions, login, logout, security, middleware]  
**Relacionados:** c1-arch-overview, c3-db-schema, c8-security-checklist  

---

## Visão Geral

O projeto usa **JWT (JSON Web Tokens)** para autenticação com sessions armazenadas no Redis.

```text
User Login Flow:
├─ POST /api/auth/login (email + password)
├─ Backend valida credenciais contra database
├─ Gera JWT token + armazena session no Redis
├─ Retorna token ao cliente
└─ Cliente armazena em httpOnly cookie

User Request Flow:
├─ Cliente envia cookie com todo request
├─ Middleware valida token
├─ Extrai user_id + permissões
└─ Permite ou nega acesso
```

---

## Implementação

### Backend (src/auth/jwt-service.ts)

```typescript
import jwt from 'jsonwebtoken';
import redis from './redis-client';

const SECRET = process.env.JWT_SECRET;

export async function createSession(userId: string) {
  const token = jwt.sign({ userId }, SECRET, { expiresIn: '7d' });
  await redis.set(`session:${userId}`, token, 'EX', 604800); // 7 days
  return token;
}

export async function validateToken(token: string) {
  try {
    const decoded = jwt.verify(token, SECRET);
    return decoded;
  } catch (error) {
    return null;
  }
}
```

### Frontend (src/hooks/useAuth.ts)

```typescript
import { useEffect, useState } from 'react';
import axios from 'axios';

export function useAuth() {
  const [user, setUser] = useState(null);
  
  useEffect(() => {
    // Token está em httpOnly cookie (automaticamente enviado)
    axios.get('/api/auth/me')
      .then(res => setUser(res.data))
      .catch(err => setUser(null));
  }, []);
  
  return { user, isAuthenticated: !!user };
}
```

---

## Fluxos de Teste

```text
✅ Login bem-sucedido
   POST /api/auth/login {"email": "test@example.com", "password": "correct"}
   → 200 + cookie com token + user data

❌ Senha incorreta
   POST /api/auth/login {"email": "test@example.com", "password": "wrong"}
   → 401 Unauthorized

⭐ Logout
   POST /api/auth/logout
   → Deleta session do Redis + cookie expirado

⭐ Token expirado
   GET /api/auth/me (com token expirado)
   → 401 + instruir client fazer refresh
```

---

## Segurança

```text
✅ Implementado:
   - JWT secreto em env variable (não hardcoded)
   - httpOnly cookies (protege contra XSS)
   - CSRF protection (token em header)
   - Rate limiting em /api/auth/login (máx 5 tentativas/min)
   - Sessions armazenadas com TTL (7 dias)

⚠️ Não implementado (futuro):
   - 2FA (two-factor auth)
   - Refresh token rotation
   - Device fingerprinting
```

---

## Debugging

Quando autenticação está quebrada:

```bash
# 1. Verificar token no Redis
redis-cli get session:{userId}

# 2. Decodificar JWT
node -e "console.log(require('jsonwebtoken').decode('{token}'))"

# 3. Verificar middleware
# Adicionar console.log em src/middleware/auth.ts

# 4. Revisar logs
tail -f logs/auth.log
```

---

## Documentação Relacionada

- Veja `c1-arch-overview.md` para contexto completo
- Veja `c8-security-checklist.md` para conformidade
- Veja `c3-db-schema.md` para tabela de users

---

**Status:** Current ✅  
**Próxima revisão:** 2024-12-14

---

## Uso Prático

### Para Copilot (Busca Automática)

```text

Usuário: "Como funciona autenticação?"

Copilot internamente:
├─ Busca semântica: "auth", "authentication"
├─ Encontra: c2-auth-system.md
├─ Carrega conteúdo
└─ Responde baseado em conteúdo real (não alucina)

```

### Para Você (Busca Manual)

```bash
# Procurar chunks sobre um tópico
grep -r "keyword" aioboss/chunks/

# Exemplo: Procurar sobre deploy
grep -r "deploy\|ci-cd\|pipeline" aioboss/chunks/
```

---

## Manutenção

### Quando Adicionar Chunks

```text
✅ Quando CONTEXT.md muda significativamente
✅ Quando nova feature/módulo é adicionado
✅ Quando débito técnico é refatorado
✅ Quando documentação fica desatualizada
```

### Quando Remover Chunks

```text
❌ Nunca remova, apenas atualize
   (histórico é importante)

✅ Marque como "Archived" se obsoleto
   (mantém contexto histórico)
```

### Fluxo de Atualização

```text
1. Context Engineer detecta mudança no código
2. Atualiza CONTEXT.md (SSOT)
3. Atualiza chunks relacionados
4. Sincroniza keywords para busca
5. Valida: busca semântica encontra o chunk?
```

---

## Struktur Esperada (Quando Operacional)

```text
aioboss/chunks/
├── c1-arch-overview.md           (150-200 linhas)
├── c2-auth-system.md              (120-180 linhas)
├── c3-db-schema.md                (100-150 linhas)
├── c4-components-structure.md      (120-180 linhas)
├── c5-api-routes.md               (150-200 linhas)
├── c6-deploy-pipeline.md          (100-150 linhas)    [Opcional]
├── c7-testing-strategy.md          (80-120 linhas)    [Opcional]
├── c8-security-checklist.md        (100-150 linhas)   [Opcional]
└── README.md                        (Este arquivo)

Total: ~900-1200 linhas de documentação
Tempo de manutenção: 30min/semana (por Context Engineer)
```

---

## Vantagens

```text
✅ Busca rápida (< 250ms)
✅ Agnóstico de plataforma (Copilot, Claude, Cursor)
✅ Versionável no git (histórico)
✅ Auditável (quem mudou o quê)
✅ Sem dependência de IA (markdown puro)
✅ Portável (copy-paste para outro projeto)
```

---

**ID:** 071225-220700  
**Status:** Directory Structure + Documentation  
**Versão:** 1.0.0  
**Próximo:** Context Engineer popula com chunks reais
