# Workflows Template — npm alignment note

Estas workflows são exemplos e ainda usam comandos `yarn` nos steps. Ao migrar para npm:

1. Converta cada comando para o equivalente `npm` conforme os scripts reais do `package.json` do destino.
   - `yarn <script>` → `npm run <script>` (ou `npm run <script> -- --args` se houver argumentos)
   - `yarn tsx ...` → `npx tsx ...` (ou script dedicado)
   - `yarn info <pkg> --json` → `npm info <pkg> --json`
   - `yarn dedupe`/`yarn constraints`/`yarn lazy ...` exigem avaliação: adapte para o comando npm/turbo disponível no projeto.
2. Atualize o cache do setup-node para `npm` e prefira `npm ci` nas instalações.
3. Valide a pipeline no CI (build/test) e ajuste conforme o stack do repositório alvo.

Mantenha este README como lembrete de que os arquivos `.yml` aqui são catálogos e requerem ajuste manual para npm.
