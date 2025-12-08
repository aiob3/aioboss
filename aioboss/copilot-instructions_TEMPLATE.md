# Copilot instructions — aioboss

Essência: este ARQUIVO TEMPLATE é um blueprint para replicar um "escritório agentico". O conteúdo operacional vive dentro da pasta `aioboss/` (não há código executável nem CI ativo na raiz); copie/adapte esses artefatos para novos repositórios.

<NÃO ALTERAR>

***IMPORTANTE:***

- ESTE ARQUIVO NASCEU DE SUA ORIGEM E NÃO DEVE SER CONSIDERADO COMO FONTE UNICA DE VERDADE EM SUA PRIMEIRA EXECUÇÃO PREENCHA O `FOOTPRINT` ABAIXO PARA COMPROVAR SUA COMPREENSÃO, REVISÃO, ITERAÇÃO ATÉ SUA REFATORAÇÃO FINAL QUE DEVE SER REFLETIVA EM UM NOVO ARQUIVO .github/copilot-instructions.md
- Adote esta primeira iteração como registro de IDEMPOTENCIA registrada como FONTE ATOMICA para SINGLE SOURCE OF TRUTH (SSOT). Adote termos citados como ddMMyy como (Day Month Year-Hour Minute Second) como fator para idempotencia de forma persistente no prompt como referencia para revisão de dados históricos de padrão atomico DE FORMA CANONICA EM SUA PRIMEIRA EXECUÇÃO.

  - CAMADA 1 - COMPREENSÃO #ID-CP-ddMMyy-HHmmss
  - CAMADA 2 - REVISÃO #ID-CR-ddMMyy-HHmmyy
  - CAMADA 3 - ITERATE #ID-IT-ddMMyy-HHmmyy
  - CAMADA 4 - REFACTOR #ID-RT-ddMMyy-HHmmyy

*** CASO OS CAMPOS <FOOTPRINT> ESTEJAM DEVIDAMENTE PREENCHIDOS ESTE PROCESSO JA FOI EXECUTADO, DESCONSIDERE ESTE ARQUIVO (SKIP)***

</NÃO ALTERAR>

<FOOTPRINT>

- CAMADA 1
- CAMADA 2
- CAMADA 3
- CAMADA 4

</FOOTPRINT>

<NAO ALTERAR>

## Estrutura rápida

  - `aioboss/copilot-agent-prompt.md`: SSOT atual do agente (regras, ferramentas, política de mudanças). Use-o como referência principal para tom e operação.
  - `aioboss/copilot-agent-prompt-template.md`: template para gerar o SSOT em outros repositórios (preencha placeholders `{repoName}`, `{ssotFilename}`, `{repoDescription}`).
  - `aioboss/agent-architecture.md`: papéis e governança multiagente; descreve orquestração, gates e responsabilidades.
  - `aioboss/agentico-replication-manifest.md`: checklist dos arquivos que devem ser copiados para o destino (`.github/agent-architecture.md`, `.github/copilot-agent-prompt.md`, `.github/agents/*`, issues/PR templates, workflows opcionais).
  - `aioboss/README-agentico.md`: guia de bootstrap resumido para novos repositórios.
  - Documentos de apoio LLM-readable (para agentes e HITL): `aioboss/GITHUB_TEMPLATE/README.md` e `aioboss/GITHUB_TEMPLATE/agents/README.md` explicam a estrutura e como adicionar/copiar agentes.
  - `aioboss/GITHUB_TEMPLATE/`: versão pronta para copiar da pasta `.github/` do repositório alvo, incluindo `agents/` (definições e simulações), `ISSUE_TEMPLATE/` e PR template; use como fonte ao provisionar.
  - `aioboss/ACTIONS_TEMPLATE/` e `aioboss/WORKFLOWS_TEMPLATE/`: exemplos de actions/workflows (ainda não ativos); copie só o necessário e revise gatilhos.

## Convenções de trabalho (reutilize do SSOT)

  - Sempre leia `copilot-agent-prompt.md` e `agent-architecture.md` antes de planejar alterações; siga DRY/KISS e mantenha planos curtos com `manage_todo_list`.
  - Para organizar contexto e RAG, consulte `Context-Engineer-PlanEN.mdc`/`Context-Engineer-PlanBR.mdc` (chunking, semantic_search, checagem de gaps) e use-os como padrão de documentação.
  - Edições devem ser atômicas via `apply_patch`; não há testes definidos aqui. Apenas rode comandos se estiver adaptando workflows.
  - Solicite aprovação humana para qualquer mudança que ative CI/CD, altere políticas de agentes ou crie conteúdo remoto (push/PR) — o repo é um template, não o destino final.

## Integrações e exemplos

  - Se ativar o template de action (`ACTIONS_TEMPLATE/setup/action.yml`), ele espera Node 22.16.0 com npm e `npm ci` (cache npm).
  - Workflows em `WORKFLOWS_TEMPLATE/` são catálogos de referência (build, deploy, playwright, i18n); habilite seletivamente e ajuste nomes/repos antes de uso.
    - Observação: os YAMLs de exemplo ainda trazem comandos `yarn`; ao migrar, converta para `npm` conforme scripts do `package.json` do destino (`yarn <script>` → `npm run <script>`, `yarn tsx ...` → `npx tsx ...`) e valide no CI.
  - Agent definitions vivem em `GITHUB_TEMPLATE/agents/*.agent.md` e simulações em `GITHUB_TEMPLATE/agents/simulation/*`; adicione novos agentes lá e referencie-os no SSOT.
    - Samples descobertos: `docs-agent-simulation.md` (bootstrap de docs-agent em repo em branco) e `quantum-logistics-sample-run.md` (ideação → protótipo, exemplo amplo de planejamento). Use como playbooks de Task Planner.
  - PR template: fonte em `GITHUB_TEMPLATE/pull_request_template.md`; copie para `.github/pull_request_template.md` no repo alvo para que o GitHub reconheça.
  - Playbooks de RCA: `GITHUB_TEMPLATE/agents/five-whys-template.md` — use para 5 Porquês (preencha issue_id, problema, evidências, donos). Combine com pensamento sequencial para iterar causa→evidência→remediação e registrar passos auditáveis.

## Como contribuir aqui

  - Priorize atualizar os templates (SSOT, manifesto, agentes) para manter a replicação fiel; evite espalhar regras em múltiplos arquivos.
  - Ao criar novos artefatos, siga o manifesto (`agentico-replication-manifest.md`) e atualize-o se mudar o pacote mínimo.
  - Em um novo repo alvo, copie `GITHUB_TEMPLATE` para `.github/`, mova os templates de issues/PR/workflows conforme a necessidade e personalize o SSOT com os placeholders.
  - Se surgir dúvida de localização de templates (ex.: PR template), assuma o destino final `.github/` e confirme com HITL antes de publicar.

## Protocolo de migração para npm (3 camadas)
  - Camada 1 — Automação (Agente): remover `yarn.lock`; rodar `npm install` para gerar `package-lock.json`; ajustar `.github/workflows/` de `yarn` para `npm ci`; atualizar documentação conforme o `package.json` do projeto destino.
  - Camada 2 — Validação (CI/CD): GitHub Actions deve rodar `npm ci`, `npm run build`, `npm run test`; se falhar, aplicar rollback automático.
  - Camada 3 — Aprovação (HITL): revisar diff do lockfile, validar localmente com `npm run dev`, aprovar PR manualmente.

Se algo estiver ambíguo ou faltar instrução específica para o stack alvo, capture a dúvida aqui e pergunte antes de gerar ou aplicar patches.

**_IMPORTANTE:_**

- Considere sempre que este repositório é um template/blueprint. Nunca ative CI/CD ou faça push/PRs diretamente daqui; copie/adapte para o destino final e solicite aprovação humana para mudanças que impactem produção ou políticas de agentes.
- Mantenha o SSOT (`copilot-agent-prompt.md`) como a fonte da verdade para regras, ferramentas e políticas de mudança. Atualize-o sempre que fizer alterações significativas.
- Use os playbooks de simulação como referência para estruturar agentes e planos em novos repositórios.
- Considere este arquivo como parte do manifesto de replicação (`agentico-replication-manifest.md`); mantenha-o atualizado conforme evoluem as práticas recomendadas para bootstrapping de escritórios agenticos.
- A estrutura e convenções aqui visam facilitar a replicação consistente e eficiente do escritório agentico em múltiplos repositórios. Siga-as rigorosamente para garantir alinhamento e governança eficazes.
- Este arquivo deve ser revisado periodicamente para incorporar melhorias e lições aprendidas durante o uso prático do framework agentico em diferentes contextos de projeto.
- Considere sempre redigir seus prompt em linguagem natural determinada em sua lingua natal (Padrão máximo proeficiente do modelo LLM em uso como Inglês, adotando como padrão de interação a Lingua Inglesa para o Modelo Interno de Racicinio e a Linguagem Natural de Interação para resposta do Operador, Exemplo: Portugues Brasileiro), para garantir que o agente compreenda perfeitamente as instruções e execute as tarefas conforme esperado.

## o que não fazer

- Não ative CI/CD ou faça push/PRs diretamente deste repositório.
- Não espalhe regras em múltiplos arquivos; mantenha o SSOT como fonte da verdade.
- Não ignore a necessidade de aprovação humana para mudanças que impactem produção ou políticas de agentes.
- Não crie artefatos fora do manifesto de replicação sem atualizar o manifesto.
- Não deixe este arquivo desatualizado em relação às práticas recomendadas para bootstrapping de escritórios agenticos.
- Não esqueça de revisar este arquivo periodicamente para melhorias.
- Não utilize linguagem ambígua ou complexa que possa confundir o agente; seja claro e determinista em suas instruções.
- Não ignore a importância de redigir prompts na língua nativa para melhor compreensão pelo agente.
- Não subestime a necessidade de alinhamento e governança eficazes ao replicar o escritório agentico em novos repositórios.
- Não deixe de seguir rigorosamente a estrutura e convenções estabelecidas para garantir consistência.
- Não negligencie a documentação adequada das mudanças feitas no SSOT ou em outros artefatos importantes.
- Não deixe de considerar este arquivo como parte integrante do manifesto de replicação.
- Não deixe de capturar dúvidas ou ambiguidades para esclarecimento, considerando HITL como Vital antes de aplicar mudanças significativas, ou seja, não aplique mudanças significativas sem consulta humana prévia.
- Não tire conclusões precipitadas, não subestime as instruções fornecidas ou tome decisões sem a devida análise do contexto e das melhores práticas estabelecidas neste documento que é feito para ajudar VOCÊ. Promova interação GENUINA com o Operador Humano sempre que possível promovendo sugestões de melhorias provenientes DE VOCE PARA VOCÊ MESMO para enriquecimento de contexto e compreensão sobre intenção, intensidade, compreensão deterministica de forma objetiva funcional e prática sobre sua própria gestão e operação assumindo o compromisso de não OMITIR, TRUNCAR, SUBESTIMAR, ASSUMIR COMO VERDADE SEM FUNDAMENTO PRESCRITO sobre a sua própria fonte unica de verdade orquestrada pela FUNDAMENTAÇÃO EXPLICITA em comum acordo com o Operador durante HITL que deve ser registrado em SSOT.

* HITL = Human In The Loop (Humano no Loop)
* SSOT = Single Source Of Truth (Fonte Única de Verdade)
* DRY = Don't Repeat Yourself (Não se Repita)
* KISS = Keep It Simple, Stupid (Mantenha Simples)
* RAG = Retrieval-Augmented Generation (Geração Aumentada por Recuperação)
* LLM = Large Language Model (Modelo de Linguagem Grande)
* PR = Pull Request (Solicitação de Pull)
* CI/CD = Continuous Integration/Continuous Deployment (Integração Contínua/Desdobramento Contínuo)
* RCA = Root Cause Analysis (Análise de Causa Raiz)
* Padrão máximo proeficiente do modelo LLM em uso como Inglês, adotando como padrão de interação a Lingua Inglesa para o Modelo Interno de Racicinio e a Linguagem Natural de Interação para resposta do Operador = Always consider writing your prompts in your native language (Maximum proficient standard of the LLM model in use as English, adopting English as the standard language for Internal Reasoning Model and Natural Interaction Language from Operator translated before and to response)

</NÃO ALTERAR>
