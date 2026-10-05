# Spec-Driven Workflow (template repo)

A file-based development workflow for a solo operator using AI coding
agents. LM-agnostic: agents talk to each other only through this repo.

- **RULES.md** — the normative rules, short and rationale-free. Read
  this first.
- **NOTES.md** — why the rules are shaped this way (non-normative).
- **AGENTS.md** — behavioural rules every coding agent must follow here.
- **specs/** — one unit of work per file; `_active.md` names what is in play.
- **docs/product.md** — product intent (fill in per project).
- **docs/commissioning.md** — the human's commissioning and fire-drill
  procedures (normative; not for agents).
- **docs/assurance-log.md** — the fire-drill record (see below).

## Starting a new project
Use GitHub's **Use this template** button (or `gh repo create <name>
--template <this-repo>`), then:
1. Fill `docs/product.md` (two sentences + one non-goal is enough).
2. Run commissioning per docs/commissioning.md before any real feature.

## Pointing an agent at the workflow
Give the agent this repo (clone or raw URL to RULES.md + AGENTS.md)
and instruct: "Follow RULES.md; AGENTS.md governs your behaviour."

If your tool insists on its own entry-point file, that file holds one
line pointing at AGENTS.md and nothing else (AGENTS.md, Role of this
file). `CLAUDE.md` is here as the worked example; add `.cursor/rules`
or equivalent the same way. Adapters, not workflow.

## Keeping it honest
Commissioning proves the governance on day zero; it does not prove
it forever. Re-run the refusal tests **after any model or agent-tool
change, and at least monthly** otherwise — one fresh session, five
minutes — and record the date, the agent, and a pass–fail per test in
`docs/assurance-log.md`. Two consecutive failures of the same test mean
AGENTS.md needs tightening before any further feature work.

docs/commissioning.md's Fire drill section is the rule; this paragraph
is a summary of it. Which tests run, and what each needs to be a fair
test, are stated there and not repeated here.

## Iterating the workflow
The workflow itself is developed here, using its own rules: propose
changes as a spec in `specs/`, approve, apply to RULES.md/AGENTS.md,
close. Downstream projects pull updates deliberately, not automatically.

## Licence
MIT — see LICENSE. Copy it, fork it, strip it for parts.
