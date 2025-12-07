# Task Planner — Simulation & Calibration (Examples)

This file contains sample inputs and the expected agent outputs for the Task Planner (Supervisor/Orchestrator). Use these examples for training, calibration, and validation.

## Example 1: High-Level Feature Request
**Input**: "Implement a new 'hand' pan tool with tests and docs"

**Expected Steps (Task Planner)**:
1. **Discovery** (Data Fetch Required)
   - `grep_search "HandTool" ` and `semantic_search "hand tool"` across codebase -> *Next agent/tool*: Context Engineer
2. **Define Work**
   - Create the work decomposition: implement tool component, update defaultTools, add example in `apps/examples`, unit tests, e2e tests -> *Next agent/tool*: Dev Agent
3. **Provision Agents & Tasks**
   - Draft `dev-agent` agent spec for tool implementation and `test-agent` for tests -> *Next agent/tool*: Task Planner (provision agent skeleton)
4. **Prepare PR skeleton**
   - Create `apply_patch` diff of README/example, tests skeleton, and a new directory for examples -> *Next agent/tool*: Dev Agent
5. **Finalize**
   - Ensure `npm run typecheck` and tests run before human review -> *Next agent/tool*: Test Agent

**Output**: Numbered sub-task list as described above, including tool/agent recommendations and 'Data Fetch Required' where applicable.  
Conclude: `<PLAN_COMPLETE>`

---

## Example 2: Provision New Agent
**Input**: "Provision a `docs-agent` to own SSOT updates and docs automation"

**Expected Steps**:
1. **Discovery** (Data Fetch Required)
   - Identify all `CONTEXT.md`, docs, and `README` locations -> *Next agent/tool*: Context Engineer
2. **Design the agent**
   - Produce a `docs-agent` skeleton with meta-instruction and simulation -> *Next agent/tool*: Task Planner
3. **Prepare provisioning**
   - Create `docs-agent.agent.md`, `docs-agent-simulation.md`, and `apply_patch` PR skeleton -> *Next agent/tool*: Task Planner
4. **Validation**
   - Run `runTests` and confirm tests pass in related docs packages -> *Next agent/tool*: Test Agent
5. **Human review**
   - Open PR for human review (Product Manager) with clear acceptance criteria -> *Next agent/tool*: Supervisor / Human Review

**Output**: Agent skeletons, PR diffs, and a plan for tests + human review with `<PLAN_COMPLETE>`

---

## Calibration guide
- Validate: the Task Planner should always enumerate sub-tasks and recommend the next agent/tool. If it suggests modifications to production or CI, it must require human approval.
- Test: run the Task Planner with a sample `issue` and confirm the pipeline of discovery → design → provision → validate steps are produced.
