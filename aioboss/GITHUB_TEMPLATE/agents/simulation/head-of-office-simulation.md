# Head-of-Office — Simulation & Calibration

## Example 1: Final approval of analytics deployment
**Input**: "Approve analytics deployment and budget for premium HandTool features."

**Steps (Head-of-Office)**:
1. Review Task Planner plan and PM's PRD.
2. Check legal/compliance flags, cost estimates, and infra needs.
3. Approve with conditions or reject and request additional documentation.
4. If approved, schedule review date and owner; log audit.

**Expected Output** (JSON):
{
  "decision": "approved",
  "conditions": ["add privacy review for analytics","set monitoring & rollback plan"],
  "owner": "product-manager",
  "reviewDate": "2025-12-20"
}

---

(End of Head-of-Office simulation.)
