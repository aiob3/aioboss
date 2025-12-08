# AIOBoss — Instruções para Copilot (curtas)

- **Natureza do repo:** é um **template de escritório agentico** (nenhum app/CI ativo). Artefatos servem para copiar/adaptar em projetos destino.
- **Leia antes de agir:** `docs/README.md` (fundação/arquitetura), `aioboss-foundation.md` (porquê/fluxo), `agent-architecture.md` (papéis/gates), `copilot-agent-prompt.md` (SSOT operacional) e `docs/00-START-HERE.md` (bootstrap).
- **Papéis e handoffs:** deduza e atue; corrente padrão = Context Engineer (mapa/CONTEXT+chunks) → Task Planner (plano) → Dev Agent (código/testes/diffs) → Head-of-Office (governança). Context Engineer roda antes/depois para manter SSOT.
- **Bootstrap em repositório alvo:** copiar `GITHUB_TEMPLATE/` para `.github/`, copiar manifestos/prompts (`copilot-agent-prompt*`, `agent-architecture.md`, `agentico-replication-manifest.md`), criar `.aioboss/CONTEXT.md` + `.aioboss/chunks/`, então rodar o prompt de ativação em `docs/00-START-HERE.md` / `example-AIOBoss-activation.md`.
- **SSOT vivo:** `CONTEXT.md` é fonte única; sempre que o estado mudar, sincronize e gere/atualize chunks seguindo `docs/chunks-README.md` (IDs cN-domain-topic, keywords, related). Use `Context-Engineer-PlanEN/BR.mdc` como checklist.
- **Templates de agentes:** `GITHUB_TEMPLATE/agents/*.agent.md` e `GITHUB_TEMPLATE/agents/simulation/*.md` definem ativação, ferramentas e handoffs. Mantenha-os alinhados ao SSOT e use `agentico-replication-manifest.md` como checklist de cópia.
- **Workflows/Ações:** itens em `WORKFLOWS_TEMPLATE/` e `ACTIONS_TEMPLATE/` são catálogos inativos; steps usam `yarn`/Node 22.16. Se habilitar em outro repo, converta para `npm` conforme `WORKFLOWS_TEMPLATE/README.md`, valide triggers e peça aprovação humana.
- **CI/build/test:** aqui não há suites nem scripts a rodar. Em destinos, siga o `package.json` local e documente comandos no CONTEXT/chunks.
- **Guardrails:** nunca invente segredos; se precisar, peça `.env.example` com placeholders. Não aplique patches em silêncio nem faça push/PR sem pedido explícito; prepare diffs (`apply_patch`) e peça revisão, especialmente para governança/CI/políticas de agentes.
- **Saídas esperadas em cada resposta:** plano curto (bullets), diffs propostos, próximos passos claros; se faltar dado do stack alvo, pergunte antes de escrever código. Mantenha rastreabilidade citando arquivos tocados e atualizando `manage_todo_list`.
- **Navegação rápida:** priorize `docs/README.md`, `agent-architecture.md`, `copilot-agent-prompt.md`, `docs/chunks-README.md` para entender decisões; use `file_search`/`read_file` para localizar.

Se algo estiver ambíguo ou faltar comando específico do projeto alvo, registre a dúvida aqui e confirme antes de editar arquivos.
