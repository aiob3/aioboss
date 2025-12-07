# Task Planner — Sample Run: quantum logistics (ideação → protótipo)

Objetivo: exemplo inicial para novos projetos em branco usando o framework agentico AIOBoss, cobrindo ideação até plano de protótipo funcional (mercado/logística quântica). Use como referência de planejamento; requer revisão humana para dados externos.

## Input

"Research the current market viability of quantum computing in logistics, analyze key players, and propose a strategic entry plan for a new startup."

## Output (Task Planner steps)

1. **Scoping & Discovery** (Data Fetch Required)
   - Determine scope (market, verticals of logistics) and gather constraints (budget, timelines). Use `semantic_search` and `web` to locate latest reports and `news` items.
   - Tools: `semantic_search`, `file_search`, `web`.
   - Next Agent/Tool: Context Engineer (for consolidated summary) / web & search

2. **Market Research & Sizing** (Data Fetch Required)
   - Gather market reports, investment trends, and adjacent technologies (quantum annealing, gate-based). Calculate TAM/SAM/SOM and trends.
   - Tools: `web`, `semantic_search`.
   - Next Agent/Tool: Analyst Agent (or use Task Planner with Data Fetch + Test Agent for validations)

3. **Competitive Mapping** (Data Fetch Required)
   - Identify key players (startups, incumbents, research labs) and their technology stacks & partnerships.
   - Tools: `web`, `semantic_search`, `file_search`.
   - Next Agent/Tool: Context Engineer (to extract any repo-relevant intel), Analyst Agent

4. **Technical Feasibility** (Data Fetch Required)
   - Analyze whether known quantum approaches (optimization, QUBO, hybrid methods) fit logistics problems (routing, scheduling). Provide short feasibility scoring for top 3 use cases.
   - Tools: `semantic_search`, `web`, `read_file` (if repo contains research), `notebook` for modeling.
   - Next Agent/Tool: Dev Agent (to prototype small models) / Notebooks

5. **Strategic Entry Plan Draft**
   - Based on previous steps, propose go-to-market: target verticals, technology stack, partnership asks, MVP definition, and nearterm roadmap.
   - Tools: `Task Planner` to compile and `Context Engineer` to validate documentation.
   - Next Agent/Tool: Task Planner -> produce final plan for human review

6. **Validation & Governance**
   - Create a checklist for regulatory concerns, IP considerations, and data privacy for the given region.
   - Tools: `web`, `file_search`, `semantic_search`.
   - Next Agent/Tool: Legal/Compliance (human) and Product Manager for approval

<PLAN_COMPLETE>

---

## Candidate Agent Work for this Plan

- Timeline & breakdown of tasks for each sub-agent (Context, Analyst, Dev, QA)
- Example artifacts: `market-research.md`, `player-analysis.csv`, `technical-feasibility.ipynb`.

## Note

- This is an example-only plan; data fetch is required and should be validated by a human reviewer before execution.
