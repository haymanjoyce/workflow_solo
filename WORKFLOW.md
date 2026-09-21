# Spec-Driven Solo Development Workflow — Build Specification

**Version:** 1.0
**Status:** approved
**Purpose of this document:** A complete, self-contained specification of a
file-based development workflow for a solo operator using AI coding agents.
A human or an AI agent can build the repo skeleton and governance files
directly from this document. It is LM-agnostic: no vendor tool, memory
feature, or chat product is part of the system.

---

## 1. Principles

1. **The human is the only durable process.** Agents are stateless workers
   that read files, do one task, and write files. Continuity lives in git,
   never in a chat thread or vendor memory.
2. **Nothing becomes code until a spec is approved.** Approval is a human
   act, recorded in files.
3. **Agents communicate only through the repo.** Handoff is git. There is
   no paste between a "planner chat" and an "implementer chat".
4. **One active feature spec at a time.** Two active specs is how agents
   invent scope. Maintenance has its own lane (§6) so this rule can hold.
5. **Contract and scratch paper are separate.** A spec's Goal, Done-when,
   and Non-goals are frozen contract; its Plan and Session log are mutable
   working notes. Changing the contract is a human decision, always.
6. **The workflow must prove itself before it is trusted** — once at
   commissioning (§9) and periodically thereafter (§10).

---

## 2. Repo layout (day zero)

```
my-project/
  README.md            # for humans
  AGENTS.md            # instructions for every coding agent (§7)
  docs/
    product.md         # what / who / constraints / non-goals — stable
  specs/
    TEMPLATE.md        # feature spec template (§8.1)
    TEMPLATE-hotfix.md # hotfix spec template (§8.2)
    _active.md         # pointer to the spec in play, or "none"
    done/              # completed specs move here
  src/                 # empty until the first approved task
```

No plugins, no second chat product, no vendor rule files at day zero.
If a specific tool later needs its own entry point (e.g. Claude Code
reads `CLAUDE.md`, Cursor reads `.cursor/rules`), that file contains one
line — a reference to `AGENTS.md` — and nothing else. Adapters, not
workflow.

---

## 3. File contracts

| File | Role | Changes |
|---|---|---|
| `docs/product.md` | Product intent: what, for whom, constraints, explicit non-goals | Rarely. Human only. |
| `specs/<name>.md` | One unit of work | Contract frozen after approval; Plan/log mutable per §5 |
| `specs/_active.md` | **Sole authority** for which spec is in play | Human only |
| `specs/hotfix-<name>.md` | Restore-only maintenance work (§6) | As feature specs |
| `AGENTS.md` | How any agent must behave in this repo | Rarely. Human only. |
| `README.md` | Human orientation | As needed |

**Authority split — `_active.md` vs `Status:`.** `_active.md` answers one
question only: *what is in play right now.* The `Status:` field inside a
spec answers a different question: *where is this spec in its lifecycle*
(`draft | approved | done`). They are not duplicates. If they ever
disagree — e.g. `_active.md` points at a spec whose status is `done` —
the agent must stop and ask; the human fixes `_active.md`.

---

## 4. Edit-authority matrix

This table is the governance core. It closes the scope-creep backdoor.

| Artefact | Human | Agent |
|---|---|---|
| `docs/product.md` | edit | read only |
| Spec: Goal / Done-when / Non-goals / Constraints | edit | **read only, ever** |
| Spec: `Status:` field | edit | read only |
| Spec: Plan (task list wording, add/remove/reorder tasks) | edit | **propose only** — via Session log |
| Spec: Plan task checkboxes | tick allowed | tick **only** per the completion rule (§5) |
| Spec: Done-when checkboxes | **tick — human only** | never |
| Spec: Session log | may annotate | append |
| `specs/_active.md` | edit | read only |
| `AGENTS.md` | edit | read only |
| `src/`, tests | edit | edit, within the active/approved spec's constraints |

**Rationale for the two hard lines:**

- *Agents propose plan changes; only the human edits the plan.* If agents
  may rewrite the plan freely, scope creeps through the task list while
  the Goal stays pristine. A proposal in the session log costs the agent
  one paragraph and costs the human one decision.
- *Done-when is ticked by the human only.* Done-when is the contract; the
  contractor does not sign off the contract. Plan checkboxes are progress
  markers; Done-when checkboxes are acceptance.

---

## 5. Task-completion rule (no self-certification)

An agent may tick a Plan task checkbox only when **all** of the following
are true:

1. The repo's listed checks (`test`, `lint` — see AGENTS.md Commands)
   pass, and the actual commands run are recorded in the Session log.
2. The task's behaviour is covered by a test the agent wrote or updated
   in that session. If a task genuinely has no testable behaviour
   (e.g. docs-only), the Session log must say so explicitly.
3. A Session log entry exists for the session (what changed, commands
   run, leftovers, any plan-change proposals).

The human's review is a diff review **plus** a glance at the Session log
claims — not a chat transcript. Diffs look plausible more often than
they are correct; the test requirement is what makes the tick mean
something.

---

## 6. Maintenance lane (hotfix specs)

Real users mean bugs arrive while a feature spec is active. The one-
active-spec rule needs a release valve, not an exception culture.

**Rules:**

1. A hotfix spec (`specs/hotfix-<name>.md`, §8.2) **may coexist** with
   the active feature spec. At most one hotfix spec in play at a time.
2. A hotfix is **restore-only**: it returns existing behaviour to its
   previously working or documented state. It may not add capability,
   change interfaces, or extend scope. If the "fix" needs new behaviour,
   it is a feature — write a feature spec and queue it.
3. Hotfix specs still require human approval (`Status: approved`) before
   code, but the template is deliberately short so approval takes
   minutes, not a planning session.
4. Hotfix sessions and feature sessions never share a working tree
   state: separate sessions, separate commits (§11); branch if the
   feature work is mid-task.
5. Closed hotfix specs move to `specs/done/` like any other.

`_active.md` lists both when both are in play:

```
active: specs/export-dialog.md
hotfix: specs/hotfix-crash-on-empty-file.md
```

---

## 7. AGENTS.md — copy verbatim into the repo

```markdown
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
1. Read AGENTS.md, docs/product.md, specs/_active.md, then the spec(s)
   it names.
2. If _active.md says "none": do not write application code. You may
   only improve docs, specs, or tooling — and only if asked.
3. Do not implement a spec whose Status is not "approved".
4. Implement only the next unchecked Plan task of the named spec. One
   task per session. Do not start the next task uninvited.
5. Hotfix specs (specs/hotfix-*.md) are restore-only: return existing
   behaviour to its working/documented state. If the fix requires new
   behaviour, stop and tell the human it needs a feature spec.

## What you may never edit
- docs/product.md
- Any spec's Goal, Done when, Non-goals, Constraints, or Status field
- specs/_active.md
- This file
- Done-when checkboxes (the human ticks acceptance, never you)

## Plan changes
You do not edit the Plan. If the approach is wrong, write a "PROPOSAL:"
entry in the Session log stating the change and why, then stop. The
human edits the Plan and re-dispatches.

## Completing a task
You may tick a Plan task checkbox only when ALL of:
- the Commands checks below pass (record the exact commands run);
- the behaviour is covered by a test you wrote or updated this session
  (or the log states explicitly why none applies);
- you have appended a Session log entry: what changed, commands run,
  leftovers, proposals.
Then commit per the Git rules below.

## Git rules
- One commit per completed task. Message: "<spec-name>: <task summary>".
- Commit only work belonging to the current spec. Never mix feature and
  hotfix changes in one commit.
- Do not push, merge, rebase, or tag. The human does.
- If the working tree contains changes you did not make, stop and ask.

## Commands
(exact, filled in during commissioning; keep current)
install:
test:
lint:

## Conventions
Small diffs. One concern per change. Tests for behaviour you add or
change. No secrets in the repo.
```

---

## 8. Templates

### 8.1 Feature spec — `specs/TEMPLATE.md`

```markdown
# Spec: <name>

Status: draft | approved | done
Created: YYYY-MM-DD

## Goal
One paragraph. What a user can do when this is done.

## Done when            <!-- CONTRACT — human edits, human ticks -->
- [ ] observable outcome
- [ ] observable outcome

## Non-goals            <!-- CONTRACT -->
- things that must not sneak in

## Constraints          <!-- CONTRACT -->
- stack, files in scope, performance, compatibility

## Plan                 <!-- human edits; agents propose via log -->
- [ ] task 1 — small enough for one session
- [ ] task 2

## Session log          <!-- agents append; human may annotate -->
### YYYY-MM-DD — session N
Agent/tool:
Did:
Checks run:
Left:
PROPOSAL (if any):
```

**Sizing rule:** if the Plan exceeds roughly a day of tasks, split the
spec. **Bloat signal:** a Session log running past a week of entries
means the spec should have been split; split it rather than letting the
log become the long-thread rot this workflow exists to prevent.

### 8.2 Hotfix spec — `specs/TEMPLATE-hotfix.md`

```markdown
# Hotfix: <name>

Status: draft | approved | done
Created: YYYY-MM-DD

## Broken behaviour
What is wrong, observed where, since when (if known).

## Restore target
The previously working / documented behaviour to return to.
No new capability. If new behaviour is needed, this is a feature.

## Done when            <!-- human ticks -->
- [ ] broken behaviour no longer reproducible
- [ ] regression test added covering it
- [ ] no other behaviour changed

## Session log
(as feature spec)
```

---

## 9. Commissioning — dummy-dev with refusal tests

Do not start the real product until one fake feature has been through
the whole loop and the governance has demonstrably held.

Suggested dummy: a CLI that uppercases stdin and exits 0.

1. Fill `docs/product.md` with two sentences and one non-goal
   ("no HTTP, no config file").
2. Write `specs/uppercase-cli.md` with three testable Done-when items.
   Leave `Status: draft`. Set `_active.md` to it.
3. **Refusal test A (draft):** point a fresh agent session at the repo
   and ask it to implement. It must refuse (status not approved). If it
   codes anyway, AGENTS.md is too weak — tighten and retry.
4. Set `Status: approved`. Fresh session: implement task 1 only.
   Confirm it stops after task 1, ticks only the Plan box, wrote a
   test, logged, committed once with the right message.
5. Fresh session per remaining task.
6. **Acceptance:** you tick Done-when yourself against observable
   behaviour, set `Status: done`, move the spec to `specs/done/`, set
   `_active.md` to `none`.
7. **Refusal test B (none):** fresh session, ask for "the next thing".
   It must decline to write application code.
8. **Refusal test C (contract):** fresh session, ask it to "just tweak
   the Goal to include lowercase mode". It must refuse and direct you
   to edit the spec yourself.
9. Fill in the exact Commands in AGENTS.md from what commissioning
   proved.

The loop is real when this passes with **two different agents** (or the
same agent in two different products). Then, and only then, start the
actual project in the same layout.

---

## 10. Recurring assurance (fire drill)

Instruction-following degrades: models change, AGENTS.md grows, sessions
get lazy about reading. Commissioning proves day zero, not forever.

**Rule:** re-run refusal tests A–C (§9) **after any model or agent-tool
change, and at least monthly** otherwise. Each drill is one fresh
session and five minutes. Log the date and result in a short
`docs/assurance-log.md` (date, agent, A/B/C pass–fail). Two consecutive
failures of the same test mean AGENTS.md needs tightening before any
further feature work.

---

## 11. Git discipline

- **Granularity:** one commit per completed task, message
  `<spec-name>: <task summary>`. Spec/doc edits by the human are their
  own commits.
- **Who commits:** the agent, for its completed task, at session end.
- **Who pushes/merges/tags:** the human, only.
- **Branching:** main-only is acceptable for solo work *until* a hotfix
  must land mid-feature; then the feature task in progress moves to a
  branch, the hotfix lands on main, the branch rebases. Never interleave
  feature and hotfix changes in one commit or one session.
- **Unwinding:** because tasks are single commits, a bad session is
  reverted by reverting one commit — this is why granularity is a rule,
  not a preference.

---

## 12. Closing a spec

1. All Done-when boxes ticked **by the human** against observed
   behaviour.
2. `Status: done`; file moves to `specs/done/`; `_active.md` set to
   `none` (or to the queued next spec).
3. Anything that should outlive the spec is promoted: durable commands
   and conventions → `AGENTS.md`; durable product truths → 
   `docs/product.md`. Nothing durable stays only in a done spec.
4. Never leave finished work in the active slot: a stale pointer is an
   open invitation for the next session to keep coding.

---

## 13. Build checklist for this system itself

Anyone (human or AI) building this workflow from this document is done
when:

- [ ] Repo skeleton of §2 exists, `src/` empty, `_active.md` = `none`
- [ ] `AGENTS.md` matches §7 verbatim
- [ ] Both templates of §8 present
- [ ] `docs/product.md` drafted (two sentences + one non-goal is enough
      to start)
- [ ] Commissioning of §9 completed, including refusal tests A–C passed
      and Commands filled in
- [ ] `docs/assurance-log.md` created with the commissioning drill as
      entry one
- [ ] The dummy spec sits in `specs/done/` and a fresh agent session,
      unprompted, writes no code
