# Manifesto de Arquivos — Escritório Agentico

Este manifesto lista os arquivos que devem ser copiados/adaptados para reproduzir o escritório Agentico em um novo repositório. Use-o como checklist para o Operador ao bootstrap do projeto.

## Núcleo de SSOT e arquitetura

- `.github/agent-architecture.md` — papéis, responsabilidades e fluxo de governança multiagente.
- `.github/copilot-agent-prompt.md` — SSOT principal do agente no repositório (regras, ferramentas, política de mudanças).
- `.github/copilot-agent-prompt-template.md` — template para gerar o SSOT em novos repositórios (preencher placeholders).
- `.github/copilot-instructions.md` — instruções gerais do repositório e ponte para o SSOT.

## Definições de agentes (pasta `.github/agents/`)

- `README.md` — instruções para adicionar novos agentes.
- `task-planner.agent.md` — orquestrador/gate para provisionar agentes.
- `context-engineer.agent.md` — responsável por SSOT, RAG e chunking.
- `dev-agent.agent.md` — implementação de código, testes e PRs.
- `product-manager.agent.md` — OKRs, backlog, aprovação de agentes/features com impacto de negócio.
- `ux-designer.agent.md` — critérios de UX/a11y, protótipos e handoff.
- `head-of-office.agent.md` — governança, compliance, sign-off de alto risco.
- Simulações e playbooks: `*-simulation.md` (context, task-planner, dev, pm, ux, head), `five-whys-template.md`.

## Suporte a templates e issues

- `.github/ISSUE_TEMPLATE/*.yml` — bug/feature/example/config (opcional, copiar se quiser o mesmo fluxo de issues).
- `.github/pull_request_template.md` — modelo de PR (se aplicável).

## Workflows de referência (opcional)

- `.github/workflows/*.yml` — automações existentes; replique apenas as necessárias ao seu processo.

## Como usar este manifesto

1) Copie os arquivos acima para o novo repositório, mantendo caminhos relativos.
2) Preencha o SSOT usando o template (`copilot-agent-prompt-template.md`) e atualize referências em `README/CONTRIBUTING`.
3) Ajuste os arquivos de agentes ao novo domínio (propósito, ferramentas, KPIs, critérios de ativação).
4) Ative apenas os workflows que fizerem sentido; revise gates de aprovação humana.

## Observação

Este manifesto deve acompanhar o pacote inicial de arquivos copiados, para que o Operador tenha visibilidade dos artefatos mínimos necessários à retomada e governança do escritório Agentico.
