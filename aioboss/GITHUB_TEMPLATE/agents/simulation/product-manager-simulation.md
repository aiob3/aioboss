# Product Manager — Simulation & Calibration

## Example 1: Prioritize feature request (HandTool)
**Input**: "Task Planner requests validation for a new `HandTool` feature with premium tier and analytics."

**Steps (PM)**:
1. Read `CONTEXT.md` and `CE` summary (Context Engineer).
2. Propose OKR: Increase activation by 10% in 2 weeks (MVP metric).
3. Assign Priority: 2 (medium-high).
4. Create PRD (short): scope, success metrics (analytics events), risk & rollback plan.
5. Check compliance/legal flags; if present, escalate to Head-of-Office.

**Expected Output** (JSON):
{
  "objective": "Release HandTool with premium analytics",
  "okr": "+10% user activation in 2 weeks",
  "priority": 2,
  "dependencies": ["dev-agent","ux-agent","context-engineer"],
  "prChecklist": ["typecheck","lint","tests","legal review if analytics"]
}

---

(End of `Product Manager` simulation)
