# Five Whys Session — Task Planner Simulation

## Input
High-level request: "Feature: Implement HandTool with premium analytics; investigate frequent drop-off during onboarding for mobile users (5% -> 2% goal)".

## Participants
- Task Planner (`<position>-tp`)
- Context Engineer (`<position>-ce`)
- Product Manager (`<position>-pm`)
- UX Designer (`<position>-ui`)
- Head-of-Office (`<position>-ho`)

## Goal
Use Five Whys to identify root cause(s) for drop-off and produce immediate remediation plan + OKRs.

## Steps (Simulated)
1. Task Planner: gathers a short statement and activates Context Engineer & PM.
   - Tools: `semantic_search`, `read_file`.
2. Context Engineer: returns context chunks: onboarding flow, analytics events, and storage of previous tests.
   - Tools: `grep_search`, `read_file`, `semantic_search`.
3. PM: clarifies business objective and asks UX for hypothesis.
   - Output: OKR: reduce onboarding drop-off from 5% to 2% within 2 sprints.
4. UX: provides immediate user-flow tests and hypothesis (tap target, animation, onboarding CTAs). Prepares initial acceptance checks.
   - Tools: `create_file` (wireframes), `read_file`.
5. Task Planner initiates Five Whys process (PM + UX + CE + HO).

### Five Whys (example answers)
1) Why are mobile onboarding users dropping off?  
   - Hypothesis: The onboarding screen has a CTA hidden or too small on mobile.
   - Evidence: CE analytics shows 80% drop at onboarding screen; UX reports small CTA.
2) Why is the CTA small/hidden?  
   - Hypothesis: A CSS change reduced hit area / responsive rules for certain devices.
   - Evidence: grep_search reveals recent change  `mobile.css` patch that removed padding.
3) Why was the CSS change deployed without UX acceptance?  
   - Hypothesis: Dev Agent implemented quick fix for a bug and the PR bypassed full review (no UX acceptance on small bug fixes).
   - Evidence: PR logs show quick fix by developer tagged as minor.
4) Why did PR bypass UX acceptance?  
   - Hypothesis: No policy to require UX sign-off for UI changes; Task Planner wasn't notified.
   - Evidence: `CONTEXT.md` lacks policy for UI sign-offs; no enforced PR template check.
5) Why lacks a PR check?  
   - Hypothesis: Legacy repo lacks automation enforcing UX sign-offs; governance oversight.
   - Evidence: `CONTRIBUTING.md` contains generic signoff; `copilot-agent-prompt.md` and `agent-architecture.md` lack explicit UX gating rule.

## Root cause (Five Whys):
- Governance/config missing for mandatory UX sign-offs (process + automation) leading to small quick fixes that break mobile UX.

## Remediation Plan (SOP) — Immediate (atomic) steps
1. Implement PR template check to require UX sign-off for any `ui/` changes. (Owner: Task Planner / Dev Agent) - Due: 2 days
2. Add an accessibility check to CI for CTA sizes and tap targets (Owner: Dev Agent / Test Agent) - Due: 1 week
3. Revert or quick-fix `mobile.css` to restore CTA area and release a patch hotfix (Owner: Dev Agent) - Due: now
4. Add `conecta-se COM`/`responde PARA` info for UX in `CONTEXT.md` and SSOT (Owner: Context Engineer) - Due: 2 days

## OKR / KPIs
- Objective: Reduce onboarding drop-off from 5% to 2% within 2 sprints.  
- KPI: Mobile onboarding 1st-week drop-off rate (Target: 2%).
- KPI: % of PRs with UX sign-off in `ui/` changes (Target: 100%).

## Validation plan

- Tests: unit for CSS rules, mobile E2E simulations using Playwright; `cd apps/examples && npm run e2e -- --grep onboarding`.
- Monitor: `analytics.onboarding.dropoff` metric and dashboard; check in 2 weeks.

## Acceptance

- All remediation steps implemented and tests pass; Head-of-Office sign-off (HO) required for any hotfix applied to production.

---

(End of Five Whys simulation session).
