# BOOTSTRAP PROMPT - Prompt Chat to Activate: AIOBoss

## O Trigger

```text
🚨 ACTIVATE AIOBOSS

Carregue os dados agênticos do #aioboss.

Siga:

1. Leia: `aioboss/agent-architecture.md`
2. Leia: `aioboss/copilot-instructions.md` (MASTER)
3. Leia: `aioboss/GITHUB_TEMPLATE/agents/*.agent.md`
4. Escanear repositório (`README.md`, `package.json`, `src/*` and main code files)
5. Gerar `aioboss/CONTEXT.md` com estado atual
6. Indexar chunks em `aioboss/chunks/`
7. Confirme quando pronto: "-- AIOBoss -- ENGAGED --"

Princípios: DRY, KISS, SSOT
Retórica: Ethos, Pathos, Logos
```

---

## O Que Esperar

Quando você digitar isso, Copilot vai:

1. **Read Phase** (2-3 min)
   - Carrega definições de agentes
   - Carrega master prompt (copilot-instructions.md)
   - Entende a arquitetura

2. **Scan Phase** (5-10 min)
   - Analisa estrutura do seu projeto
   - Identifica tech stack
   - Mapeia módulos principais
   - Detecta gaps

3. **Index Phase** (5-10 min)
   - Cria CONTEXT.md (SSOT vivo)
   - Gera chunks para RAG
   - Sincroniza memória

4. **Confirmation** (< 1 min)
   - Confirma: "✅ AIOBoss ENGAGED"
   - Pronto para receber tarefas

- **Total: ~20-30 minutos para projeto novo ou em caos**

---

## Próximas Instruções (Após "-- AIOBoss -- ENGAGED --")

Agora você tem um **virtual dev team**. Exemplos:

```text
Você: "Qual é o estado atual do meu projeto?"
Copilot (Context Engineer): [Retorna relatório de CONTEXT.md]

Você: "Preciso implementar autenticação OAuth2. Qual é o plano?"
Copilot (Task Planner): [Quebra em 5-7 sub-tasks]

Você: "Implementa a task 1 (setup OAuth2 provider)"
Copilot (Dev Agent): [Cria código + testes + diffs]

Você: "Review antes de merge?"
Copilot (Head-of-Office): [Aprova ou solicita ajustes]
```

---

## Quando Usar

- ✅ Novo projeto que você quer estruturar com context engineering
- ✅ Projeto existente que você quer "resgatar" do caos
- ✅ Projeto que cresceu e você perdeu a arquitetura
- ✅ Quando Copilot começa a alucinar (falta contexto)
- ✅ Antes de escalar (contratar devs, delegar tarefas)

---

## Reset / Rescan

Se você quer que AIOBoss **rescaneie** (código mudou bastante):

```text
🔄 RESCAN AIOBoss

Atualize o estado do projeto:
1. Re-escanear repositório
2. Atualizar aioboss/CONTEXT.md
3. Re-indexar chunks
4. Confirme: "✅ CONTEXT REFRESHED"
```

---

**ID:** 071225-220700
**Versão:** 1.0.0
**Status:** Ready to Copy-Paste
