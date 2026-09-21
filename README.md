# Spec-Driven Workflow (template repo)

A file-based development workflow for a solo operator using AI coding
agents. LM-agnostic: agents talk to each other only through this repo.

- **WORKFLOW.md** — the normative specification. Read this first.
- **AGENTS.md** — behavioural rules every coding agent must follow here.
- **specs/** — one unit of work per file; `_active.md` names what is in play.
- **docs/product.md** — product intent (fill in per project).

## Starting a new project
Use GitHub's **Use this template** button (or `gh repo create <name>
--template <this-repo>`), then:
1. Fill `docs/product.md` (two sentences + one non-goal is enough).
2. Run commissioning per WORKFLOW.md §9 before any real feature.

## Pointing an agent at the workflow
Give the agent this repo (clone or raw URL to WORKFLOW.md + AGENTS.md)
and instruct: "Follow WORKFLOW.md; AGENTS.md governs your behaviour."

## Iterating the workflow
The workflow itself is developed here, using its own rules: propose
changes as a spec in `specs/`, approve, apply to WORKFLOW.md/AGENTS.md,
close. Downstream projects pull updates deliberately, not automatically.
