# Five Whys — Template (Root Cause Analysis)

## Purpose
Template para executar sessões "Five Whys" (5 Porquês) de forma padronizada, LLM-Readable e com registro para auditoria.

## Template (LLM-friendly)
- `issue_id`: {ISSUE-1234}
- `title`: {Short title}
- `initiator`: {agent or user}
- `date`: {YYYY-MM-DD}

### Problem Statement
- `problem`: {Describe the problem in one or two sentences}

### Five Whys (Iterative)
1) Why #1: {root cause hypothesis 1}  
   - Evidence: {link(s) to file / logs / CE chunks}  
   - Owner: {agent or human}  
2) Why #2: {why #1 leads to this cause}  
   - Evidence: ...  
   - Owner: ...  
3) Why #3: {why #2 leads}  
   - Evidence: ...  
   - Owner: ...  
4) Why #4: {why #3 leads}  
   - Evidence: ...  
   - Owner: ...  
5) Why #5 (root): {core root cause}  
   - Evidence: ...  
   - Owner: ...

### Remediation Plan (SOP)
- Steps (atomic):  
  1. {step 1} - Owner: {human/agent} - Due: {YYYY-MM-DD}  
  2. {step 2} - ...

### OKRs & KPIs
- `OKR` : {Objective + Key result}  
- `KPI` : {Metric to measure fix effectiveness}  

### Validation & Acceptance
- `tests`: {list of tests/commands to validate fix}  
- `monitoring`: {metric names, dashboards}  
- `audit evidence`: {logs, PR links, acceptance review}

### Conclusion & Notes
- `final_verdict`: {resolved / follow-up required}
- `finalized_by`: {agent/human}
- `finalized_on`: {YYYY-MM-DD}

---

Use esse template para guiar sessões e registrar causal analysis de forma padronizada e auditável.
