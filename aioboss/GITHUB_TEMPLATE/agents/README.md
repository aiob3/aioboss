# Agents Directory

This directory contains sub-agent definitions and templates used for agentic operations within the tldraw repository.

Usage:

## Agents

- `task-planner.agent.md` — the Task Planner (Senior Supervisor/Orchestrator).
- `product-manager.agent.md` — the Product Manager (Senior, Head Growth).
- `context-engineer.agent.md` — the Context Engineer sub-agent (Senior).
- `ux-designer.agent.md` — the UX Designer (Senior).
- `dev-agent.agent.md` — the Dev Agent (Senior).
- `head-of-office.agent.md` — the Head-of-Office (Senior Supervisor).

## Simulation

- Cada perfil agentico possui seu perfil de simulação localizado em `simulation/<agent>-simulation.md`

## Adding new agents

1. Create a file under `GITHUB_TEMPLATE/agents/` (copiado depois para `.github/agents/` do repo destino) with `NAME.agent.md` extension.
2. Define the activation flow, tools, handoffs, and acceptance criteria.
3. Add a simulation file to check invocations and a test/guide for human validation.
4. Add `five-whys-template.md` for root cause analysis and auditability.
