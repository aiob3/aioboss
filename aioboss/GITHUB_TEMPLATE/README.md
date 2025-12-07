# Agents Directory

This directory contains sub-agent definitions and templates used for agentic operations within the tldraw repository.

Usage:

## Agents

- `agents/task-planner.agent.md` — the Task Planner (Senior Supervisor/Orchestrator).
- `agents/product-manager.agent.md` — the Product Manager (Senior, Head Growth).
- `agents/context-engineer.agent.md` — the Context Engineer sub-agent (Senior).
- `agents/ux-designer.agent.md` — the UX Designer (Senior).
- `agents/dev-agent.agent.md` — the Dev Agent (Senior).
- `agents/head-of-office.agent.md` — the Head-of-Office (Senior Supervisor).

## Adding new agents

1. Create a file under `GITHUB_TEMPLATE/agents/` (copiado depois para `.github/agents/` do repo destino) with `NAME.agent.md` extension.
2. Define the activation flow, tools, handoffs, and acceptance criteria.
3. Add a simulation file to check invocations and a test/guide for human validation.
4. Add `agents/five-whys-template.md` for root cause analysis and auditability.

## Simulation

- Cada perfil agentico DEVE possuir seu perfil de simulação para operação localizado em `agents/simulation/<agent>-simulation.md`
