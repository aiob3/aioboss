# README — Escritório Agentico (Bootstrap)

Guia rápido para configurar um novo repositório com a estrutura Agentico baseada no SSOT existente.

## Objetivo

Fornecer passos e arquivos mínimos para replicar o escritório Agentico em um novo projeto, garantindo governança, prompts consistentes e handoffs claros entre agentes.

## Arquivos essenciais

- `GITHUB_TEMPLATE/copilot-agent-prompt.md` — SSOT principal do agente (regras, ferramentas, operações) a ser copiado para o novo repo.
- `GITHUB_TEMPLATE/copilot-agent-prompt-template.md` — modelo para gerar o SSOT específico do novo repo (preencha os placeholders).
- `GITHUB_TEMPLATE/agent-architecture.md` — papéis, responsabilidades, fluxos de aprovação e escalonamento.
- `GITHUB_TEMPLATE/agentico-replication-manifest.md` — checklist completo dos artefatos que devem ser copiados/adaptados.
- Pasta `GITHUB_TEMPLATE/agents/` — definições de subagentes (`task-planner`, `context-engineer`, `dev-agent`, `product-manager`, `ux-designer`, `head-of-office`) e simulações/playbooks.

## Como usar o template de SSOT

1. Copie `GITHUB_TEMPLATE/copilot-agent-prompt-template.md` para o novo repositório como `.github/copilot-agent-prompt.md`.
2. Preencha os placeholders `{repoName}`, `{ssotFilename}`, `{repoDescription}` e ajuste ferramentas/comandos conforme o stack do novo projeto.
3. Referencie o SSOT em `README`/`CONTRIBUTING` do novo repo para descoberta fácil.
4. Mantenha `CONTEXT.md` atualizado e alinhado ao SSOT.

## Papéis e governança (resumo)

- **Task Planner**: orquestrador/gate para provisionar novos agentes e planos.
- **Context Engineer**: mantém SSOT, RAG/chunking e contexto.
- **Dev Agent**: implementa código e testes conforme plano.
- **Product Manager**: backlog, OKR e aprovação de agentes/features com impacto de negócio.
- **UX Agent**: critérios de UX/a11y e protótipos.
- **Head-of-Office**: governança e sign-off para CI/CD, produção e budget.

Gates: mudanças em produção/CI ou de alto risco exigem aprovação explícita (HO/PM). Criação de agentes passa pelo Task Planner.

## Convenções operacionais (DRY/KISS)

- Sempre ler contexto antes de agir: `CONTEXT.md`, SSOT, arquivos relevantes.
- Planejar multi-step com `manage_todo_list`; aplicar mudanças com `apply_patch` em pequenos blocos.
- Rodar testes direcionados (`runTests`/`run_in_terminal`) e evitar suites monorepo completas sem necessidade.
- Ações remotas (PR/push) só com autorização explícita; incluir typecheck/lint/testes.

## Passos de bootstrap sugeridos

1. Copiar os arquivos listados em `GITHUB_TEMPLATE/agentico-replication-manifest.md` para o novo repo, preservando caminhos.
2. Preencher o SSOT a partir do template e ajustar comandos/ferramentas ao stack alvo.
3. Revisar cada agente em `GITHUB_TEMPLATE/agents/` e adaptar propósito/KPIs/ativação ao novo domínio.
4. Atualizar `README/CONTRIBUTING` do novo repo apontando para o SSOT e para o manifesto.
5. Ativar apenas os workflows de CI necessários; revisar política de aprovação humana.

## Checklist rápido

- [ ] SSOT criado a partir do template e referenciado em `README/CONTRIBUTING`.
- [ ] `CONTEXT.md` presente e alinhado com o SSOT.
- [ ] Arquivos de agentes copiados e adaptados (incluindo simulações e `five-whys-template.md`).
- [ ] Manifesto revisado para garantir nenhum artefato faltante.
- [ ] Comandos de qualidade/testes ajustados para o novo stack.

## Nota final

Use este README como ponto de partida no novo repositório. O SSOT (`copilot-agent-prompt.md`) continua sendo a fonte canônica para comportamento de agentes, ferramentas e governança.
