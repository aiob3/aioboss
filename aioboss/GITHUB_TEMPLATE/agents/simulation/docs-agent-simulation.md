# Task Planner — Sample Run: docs-agent bootstrap

Objetivo: referência inicial (repo em branco) para provisionar um `docs-agent` no framework agentico AIOBoss. Use como simulação do Task Planner e peça revisão humana antes de publicar.

## Input

"Provision a `docs-agent` to maintain docs and SSOT and add onboarding tests and a CI check that ensures `CONTEXT.md` is up-to-date."

## Output (Task Planner steps)

1. **Discovery** - Find all docs and SSOT related files and detect current state.
   - Tools: `file_search` `grep_search` `semantic_search` `read_file`
   - Next Agent/Tool: Context Engineer
   - Data Fetch Required: Yes

2. **Design Agent** - Draft the `docs-agent` skeleton with purpose, activation criteria, tools, and AC.
   - Tools: `apply_patch` `create_file` `manage_todo_list`
   - Next Agent/Tool: Task Planner (provision agent skeleton)
   - Data Fetch Required: No

3. **Provisioning Plan** - Create provisioning artifacts: agent file, simulation, test harness skeleton, PR draft. Include a CI check to validate `CONTEXT.md` existence and minimal content (must contain `SSOT` pointers).
   - Tools: `apply_patch` `create_file` `runTests`
   - Next Agent/Tool: Dev Agent & Test Agent
   - Data Fetch Required: No

4. **Validate** - Validate the onboarding tests and simulation run of the new agent using the sample docs. Create necessary unit tests and add the PR with the skeleton to be human-reviewed.
   - Tools: `runTests`, `get_errors`, `run_in_terminal`
   - Next Agent/Tool: Test Agent
   - Data Fetch Required: No

5. **Finalize** - Ensure the PR contains `npm run typecheck` and `npm run lint`, and gather all necessary sign-offs; schedule a review with Product Manager for final approval.
   - Tools: `mcp_github_*` (PR creation requires explicit human confirmation)
   - Next Agent/Tool: Human Review / Product Manager
   - Data Fetch Required: No

<PLAN_COMPLETE>

---

## Candidate Agent Spec (partial): `docs-agent` (to be created by Task Planner)

- Purpose: Maintain repository documentation and SSOT, auto-verify `CONTEXT.md`, and generate human-facing documentation updates.
- Activation Criteria: run on PRs modifying `CONTEXT.md`, docs folder, or when `Task Planner` identifies a docs-related task.
- Tools: `file_search`, `read_file`, `apply_patch`, `semantic_search`, `runTests` (docs), `mcp_github_*` (draft PR only with permission).
- Acceptance Criteria: Includes at least one simulation example and test harness; PR passes `npm run typecheck`, `npm run lint` and relevant `runTests`.



## Notes

- The Task Planner must include traceable reasons for the agent creation and a robust plan for onboarding.
