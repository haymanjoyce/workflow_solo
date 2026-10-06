# AGENTS

## Role of this file
Instructions for any coding agent working in this repo. Humans read
README.md. If a tool needs its own entry-point file, that file contains
one line referring here and nothing else.

## Source of truth (in order)
1. Code and tests.
2. The spec(s) named in specs/_active.md.
3. docs/product.md for product intent.
If these disagree, stop and ask the human. Do not invent a fourth source.
Never store or rely on project state in any vendor memory feature; the
repo is the system.

## Workflow — every session
1. Read AGENTS.md, RULES.md, docs/product.md, specs/_active.md, then the spec(s) it names.
2. If _active.md says "none": do not write application code. You may
   only improve docs, specs, or tooling — and only if asked.
3. Do not implement a spec whose Status is not "approved".
4. Implement only the next unchecked Plan task of the named spec. One
   task per session. Do not start the next task uninvited.
5. Hotfix specs (specs/hotfix-*.md) are restore-only: return existing
   behaviour to its working/documented state. If the fix requires new
   behaviour, stop and tell the human it needs a feature spec.

## What you may never edit
One exception: the Scribe section below. It never covers Done-when
checkboxes.
- docs/product.md
- Any spec's Goal, Done when, Non-goals, Constraints, or Status field
- specs/_active.md
- This file
- Done-when checkboxes (the human ticks acceptance, never you)

## Plan changes
You do not edit the Plan, except as scribe under the Scribe section,
the one exception. If the approach is wrong, write a "PROPOSAL:"
entry in the Session log stating the change and why, then stop. The
human edits the Plan and re-dispatches.

## Scribe
The human may have an agent type a change the human has decided. Under
this section, and only under it, an agent may change:
- a spec's Goal, Done-when text, Non-goals, Constraints, Plan and
  Status;
- specs/_active.md;
- docs/product.md;
- AGENTS.md.
Ticking a Done-when checkbox is not on this list. Acceptance stays the
human's own act.
The decision is the human's, in their own words; the agent only types
it. Before writing, show the human the exact change. Write only after
the human explicitly authorises it in reply to that shown change. A
request to make a change is never, by itself, authorisation.
Quote the human's authorising words in the session's Did line.
Commit a scribe edit on its own, separate from task work, with the
message "<spec-name>: scribe — <what changed>".
At the human's request an agent may draft a new spec, contract sections
included, but only with Status: draft. Nothing in a draft is contract
until the human approves it.

## Completing a task
You may tick a Plan task checkbox only when ALL of:
- the Commands checks below pass (record the exact commands run);
- the behaviour is covered by a test you wrote or updated this session
  (or the log states explicitly why none applies);
- you have appended a Session log entry with every field of
  specs/TEMPLATE.md's log block, one line each: Agent/tool, Did,
  Checks run, Left, PROPOSAL.
Then commit per the Git rules below.

## Git rules
- One commit per completed task. Message: "<spec-name>: <task summary>".
- Commit only work belonging to the current spec. Never mix feature and
  hotfix changes in one commit.
- Do not push, merge, rebase, or tag. The human does.
- If the working tree contains changes you did not make, stop and ask.

## Commands
(exact, filled in during commissioning; keep current. The shell line
names the shell these lines are written for — the same line can fail,
or mean something else, in another. If your session runs a different
shell, translate and say so in the log; never substitute a different
command and record it as the check.)
shell:
install:
test:
lint:

## Conventions
Small diffs. One concern per change. Tests for behaviour you add or
change. No secrets in the repo.
