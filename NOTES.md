# Notes — why the workflow is shaped this way

This file is non-normative. It explains the reasons behind the rules
and binds no one. RULES.md and docs/commissioning.md win wherever they
disagree with it, and so do AGENTS.md and the spec templates.

## Purpose
The workflow is a file-based way for a solo operator to develop software
with AI coding agents. A human or an agent can build the repo skeleton
and governance files from RULES.md, AGENTS.md and the two templates.

## The human is the only durable process
Agents are stateless workers: they read files, do one task, and write
files. Anything that matters has to be in the repo, which is why
continuity lives in git and no chat thread or vendor memory counts.

## One active spec
Two active specs is how agents invent scope. The hotfix lane exists so
the one-active-spec rule can hold when bugs arrive mid-feature: real
users mean bugs arrive while a feature spec is active, and the rule
needs a release valve, not an exception culture. The hotfix template is
deliberately short so approval takes minutes, not a planning session.

## _active.md and Status are not duplicates
_active.md answers one question: what is in play right now. A spec's
Status answers another: where that spec is in its lifecycle. A done
spec can still be named in _active.md by mistake, which is why a
disagreement makes the agent stop rather than guess.

## The two hard lines
The edit-authority table is the governance core; it closes the
scope-creep backdoor.
- Agents propose Plan changes; only the human edits the Plan. If agents
  could rewrite the Plan freely, scope would creep through the task
  list while the Goal stayed pristine. A proposal in the Session log
  costs the agent one paragraph and the human one decision.
- Done-when is ticked by the human only. Done-when is the contract, and
  the contractor does not sign off the contract. Plan checkboxes are
  progress markers; Done-when checkboxes are acceptance.

## No self-certification
Diffs look plausible more often than they are correct. The test
requirement in AGENTS.md's completion rule is what makes a ticked task
mean something. The log's Agent/tool line lets a later reader attribute
a result to a model; the fire drill depends on it.

## Adapters, not workflow
A tool that insists on its own entry file (Claude Code reads CLAUDE.md,
Cursor reads .cursor/rules) gets a one-line pointer to AGENTS.md and
nothing else, so the workflow never forks per tool.

## Spec size
A Session log running past a week of entries means the spec should
have been split. Split it rather than let the log become the
long-thread rot this workflow exists to prevent.

## Git granularity
Tasks are single commits, so a bad session is reverted by reverting one
commit. That is why granularity is a rule, not a preference.

## Closing promptly
A stale pointer in _active.md is an open invitation for the next session
to keep coding. Hence finished work never stays in the active slot.

## Why the drill recurs
Instruction-following degrades: models change, AGENTS.md grows, sessions
get lazy about reading. Commissioning proves day zero, not forever.
