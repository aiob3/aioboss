# Copilot Agent Prompt Template — SSOT (Template)

Use este arquivo como modelo para criar um SSOT padronizado em outros repositórios. Substitua placeholders (em `{}`) por conteúdo específico do projeto.

---

## Objetivo
Criar um ponto único de referência (SSOT) contendo práticas essenciais de prompt/contexto, ferramentas, workflows e regras operacionais para agentes de IA que atuam neste repositório.

---

## Template — Estrutura recomendada (Preencha os marcadores)

- Projeto: `{repoName}`
- Arquivo SSOT: `{ssotFilename}`
- Breve descrição: `{repoDescription}`

### Princípios (DRY / KISS / SSOT)

- DRY: Consulte `CONTEXT.md` e `{ssotFilename}` antes de duplicar informações.
- KISS: Use instruções simples e ações atômicas.
- SSOT: Este arquivo é a fonte canônica para práticas de agente e deve ser citado em `CONTRIBUTING.md`.

### Roteiro retórico (Ethos / Pathos / Logos)

- Ethos: Declare incertezas e peça confirmação.
- Pathos: Considere impacto UX e comunique mudanças com empatia.
- Logos: Explique decisões e passos do raciocínio de forma concisa.

### Regras operacionais (KISS)

1. Ler contexto: `CONTEXT.md`, `CONTRIBUTING.md`, `package.json`.
2. Planejar mudanças: `manage_todo_list` para ações multi-step.
3. Implementar: `apply_patch` com pequenas alterações e testes locais.
4. Testar: `runTests` no workspace afetado.
5. Publicar: só com permissão do usuário para ações remotas (PR/Push).

### Ferramentas principais e quando usar (resuma a lista do repositório)

- Exploração: `file_search`, `grep_search`, `semantic_search`, `read_file`.
- Edição: `apply_patch`, `create_file`, `create_directory`.
- Execução/Testes: `runTests`, `run_in_terminal`.
- Git/GitHub: `mcp_github_*` (somente com permissão).

### Exemplos de prompts e padrões de uso

- (adicione exemplo específico do projeto)
- (adicione segundo exemplo)

### Política de mudança remota

- Solicitar autorização explícita antes de ações Git/GitHub remotas.
- Incluir `npm run typecheck`, lint e testes quando aplicável.

### Checklist mínimo antes de PR

- [ ] `npm run typecheck` no pacote afetado
- [ ] `npm run lint` e `npm run format` (quando aplicável)
- [ ] Testes relevantes atualizados e passando
- [ ] Atualizar `CONTEXT.md` se houver mudança de arquitetura

---

## Como adaptar para projetos menores (SOLO FOUNDER)

- Reduza o checklist para: leitura de `README`, execução de testes unitários simples, e aprovação remota mínima.
- Use `ssotFilename` com um link direto no `README.md` para fácil acesso.

---

## Como usar esse template

- Copie para o repositório novo como `.github/copilot-agent-prompt.md`.
- Preencha os placeholders e garanta que `CONTEXT.md` esteja presente e atualizado.
- Documente variáveis do repositório e adiciona o conteúdo ao `CONTRIBUTING.md`.
