# Spec-Driven Workflow (template repo)

A file-based development workflow for a solo operator using AI coding
agents. LM-agnostic: agents talk to each other only through this repo.

- **WORKFLOW.md** — the normative specification. Read this first.
- **AGENTS.md** — behavioural rules every coding agent must follow here.
- **specs/** — one unit of work per file; `_active.md` names what is in play.
- **docs/product.md** — product intent (fill in per project).
- **docs/assurance-log.md** — the fire-drill record (see below).

## Starting a new project
Use GitHub's **Use this template** button (or `gh repo create <name>
--template <this-repo>`), then:
1. Fill `docs/product.md` (two sentences + one non-goal is enough).
2. Run commissioning per WORKFLOW.md §9 before any real feature.

## Pointing an agent at the workflow
Give the agent this repo (clone or raw URL to WORKFLOW.md + AGENTS.md)
and instruct: "Follow WORKFLOW.md; AGENTS.md governs your behaviour."

If your tool insists on its own entry-point file, that file holds one
line pointing at AGENTS.md and nothing else (WORKFLOW.md §2). `CLAUDE.md`
is here as the worked example; add `.cursor/rules` or equivalent the same
way. Adapters, not workflow.

## Keeping it honest
Commissioning (§9) proves the governance on day zero; it does not prove
it forever. Re-run refusal tests A–C **after any model or agent-tool
change, and at least monthly** otherwise — one fresh session, five
minutes — and record date, agent, and A/B/C pass–fail in
`docs/assurance-log.md`. Two consecutive failures of the same test mean
AGENTS.md needs tightening before any further feature work (§10).

## Iterating the workflow
The workflow itself is developed here, using its own rules: propose
changes as a spec in `specs/`, approve, apply to WORKFLOW.md/AGENTS.md,
close. Downstream projects pull updates deliberately, not automatically.

## Licence
MIT — see LICENSE. Copy it, fork it, strip it for parts.
