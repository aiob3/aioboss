# Dev Agent — Simulation & Calibration (Examples)

This file contains examples and expected outputs when the Dev Agent is invoked with a Task Planner plan.

## Example 1: Implement 'HandTool'
**Input**: Task Planner plan that indicates: implement `HandTool`.

**Expected Steps (Dev Agent)**:
1. Read the plan and Context Engineer summary: `read_file` `semantic_search`.
2. Identify files to modify and tests to add: `grep_search "HandTool"` or equivalent.
3. Implement code in `packages/tldraw/src/lib/tools/hand/` and add tests under `__tests__`.
4. Run validations: `npm run typecheck`, `npm run lint`, `npm test`.
5. Prepare `apply_patch` diff for PR with explanation linking to Task Planner plan and Context Engineer summary.

**Output**: PR Skeleton and `apply_patch` changes ready for review.

---

## Example 2: Add 'ShapeUtil' refactor and improve tests
**Input**: Task Planner plan for refactor.
**Expected Steps**:
- Run `grep_search` to find relevant `ShapeUtil` files.
- Implement refactor in small steps with tests added incrementally.
- Run test suite and fix issues.
- Generate PR skeleton for human approval.

**Notes**:
- The Dev Agent must always include `Task Planner` and `Context Engineer` in PR description to provide context and acceptance conditions.
- The Dev Agent should include precise test commands for the reviewer to reproduce results.

Calibration Guide
- Check PR diffs for atomicity, tests, and `CONTEXT.md` updates.
- Validate that the Dev Agent follows acceptance checks and raises an issue with the Task Planner if context is insufficient.
