# Agent Architecture — Guia de Estrutura e Próximos Passos

Este arquivo define a arquitetura e o plano de escalonamento para a criação de agente(s) e sub-agentes alinhados ao SSOT do projeto.

## Objetivo
Descrever papéis, responsabilidades e interações para montar uma equipe de agentes e sub-agentes com foco em engenharia de contexto para replicabilidade e crescimento.

## Papéis sugeridos (e responsabilidades)
- Gerente de Produto (Product Owner): levantamento de requisitos, documentação, prioridades, backlog.
- Engenheiro de Prompt/Context (Context Engineer): criar e manter SSOT, template de prompts, recuperação de contexto (RAG), verificação de contexto e política de chunking.
- Engenheiro de Software (Dev Agent): alterações de código, testes, automações de CI.
 - Engenheiro de Software (Dev Agent): alterações de código, testes, automações de CI. This role should be a Senior-level agent capable of implementing Task Planner instructions, producing tests, and preparing PRs with clear linkages back to Task Planner and Context Engineer.
- Arquiteto UI/UX (UX Agent): revisão de UX, acessibilidade e preflight para mudanças visuais.
- QA/Tester (Test Agent): rodar suites de teste, validar e regressões.
- Gerente de Lançamento (Release Manager): orquestrar o CI/CD e publicar artefatos.
- Orquestrador de Agentes (Supervisor Agent): mission control — aprova, distribui tarefas e monitora execução e logs.
- Observabilidade/Telemetry (Ops Agent): coleta logs, métricas e geração de alertas.

- Gerente de Produto (Product Manager - `<position>-pm`): owner de PRDs, OKR, priorização e validação de business impact; conecta-se COM Task Planner, Context Engineer e Dev; responde PARA Head-of-Office.
- Head-of-Office (Head - `<position>-ho`): governança e sign-off final para infra/CI/CD e decisões de alto impacto; conecta-se COM Product Manager, Task Planner e Dev; responde PARA Stakeholder.

**Task Planner (Senior Supervisor/Orchestrator)**: A highly senior agent responsible for planning, diagnosing, and provisioning agents and sub-agents. This agent centralizes the activation and delegation of tasks and owns the policy for agent creation and onboarding. It must produce traceable plans, validate SSOT adherence, and ensure rigorous acceptance criteria for agent provisioning.

## Padrão de Interação Agente → Ferramenta → Tarefa
1. Entrada: deve conter justificativa (Ethos), impacto usuário (Pathos), e plano lógico (Logos).
2. Ações atômicas e revertíveis: sempre usar `apply_patch` para mudanças locais com testes.
3. Registro: cada ação cria/atualiza uma task no backlog (Product Manager) com justificativa.
 - Routing policy: each agent should declare `conecta-se COM` and `responde PARA` as part of their metadata for routing and ownership.
4. Escalonamento: quando ações tocam API pública, production assets, ou mudanças de configuração do CI, requer revisão humana do Product Manager e/ou Release Manager.

## Fluxo de trabalho exemplificado
1. Dev Agent solicita: “Melhorar performance do render para shapes.”
2. Orquestrador (Supervisor Agent) faz pre-check (leitura de `CONTEXT.md`, testes rápidos `runTests --grep perf`).
3. Se OK: atribui a Eng. de Software e Eng. de Prompt para revisão.
4. Eng. de Software implementa mudanças com `apply_patch` e `runTests`.
5. QA roda suite de testes e reporta via backlog.
6. Release Manager orquestra o merge e publicação.

## Técnicas e padrões de prompt e contexto
- RAG (retrieval-augmented generation): use `semantic_search` com `CONTEXT.md` para resumir e reduzir contexto.
- Chunking: dividir documento longo em tópicos com ids e mantenha sumário no SSOT para recuperação.
- Prompt Chaining & Memory: criar prompts curtos que referenciem escopos e outputs prévios.
- Minimizar a repetição: referencie SSOT e `CONTEXT.md` em vez de repetir instruções.

## Plano de implementação
1. Consolidar SSOT atual (este repositório) e transformá-lo em template universal (`copilot-agent-prompt-template.md`).
2. Criar um processo de 'bootstrap' que crie o SSOT automaticamente em novos repositórios com verificação de `CONTEXT.md`.
3. Configurar includes/links em `CONTRIBUTING.md` e `README.md` para garantir descoberta.
4. Criar orquestrador (Supervisor Agent) que coordene tarefas e logs, use filas (backlog) e verificação humana para ações de alto impacto.

## Checklist Técnico para escalar agente
- [ ] Criar `copilot-agent-prompt-template.md` (feito)
- [ ] Criar orquestrador com integrações GitHub (PR/Issues) e Webhooks
- [ ] Implementar logs, métricas e verificação em CI
- [ ] Definir gatilhos para solicitações de aprovação manual
- [ ] Documentar playbook de falhas e rollback

## Exemplo de métricas / observabilidade
- Latência de execução (ms)
- % de ações com aprovação manual
- % de PRs criadas sem testes
- Falhas de build por tipo de agente

---

Este documento é um plano inicial que pode ser ajustado para particularidades de cada projeto. Ele deverá ser mantenido pelo Eng. de Prompt/Context em colaboração com o Product Manager.
