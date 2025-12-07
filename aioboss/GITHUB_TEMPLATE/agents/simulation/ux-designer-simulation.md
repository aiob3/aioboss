# UX Designer — Simulation & Calibration

## Example 1: Mobile behaviour for HandTool
**Input**: "Design mobile behaviour for new `HandTool` with animation and haptic feedback."

**Steps (UX)**:
1. Inspect CE summaries and PRD from PM.
2. Produce wireframe and short prototype (code snippet) illustrating mobile gesture behaviour.
3. Provide acceptance criteria: animation timing, hit-area size, haptic feedback thresholds.
4. Produce accessibility checklist items and test steps for QA Agent.

**Expected Output** (JSON):
{
  "objective": "Define mobile UX for HandTool",
  "deliverables": ["wireframe.png","handtool-mobile-prototype.tsx","a11y-checklist.md"],
  "acceptance": ["animation <= 150ms","tap target >= 44px","no aria-live issues"],
  "handoff": "dev-agent"
}

---

(End of `UX Designer` simulation)
