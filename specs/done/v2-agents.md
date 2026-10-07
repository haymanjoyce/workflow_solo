# Spec: v2-agents

Status: done
Created: 2026-10-05

## Goal
The human can satisfy "fresh session per task" by having a session
dispatch the next Plan task to a fresh-context subagent, instead of
closing one session and opening another by hand. Before the human
ticks any Done-when box on a feature spec, a reviewer running a
different model from the implementing sessions reads the spec, the
diff and the Session log. It records a verdict per Done-when item. The
human ticks only once that review exists, or after logging a waiver
with a reason.

## Done when            <!-- CONTRACT — human edits, human ticks -->
- [x] RULES.md defines a fresh session as either a new session or a
      subagent whose context holds none of the dispatching session's
      conversation, given only the fixed dispatch prompt. It names no
      vendor's mechanism
- [x] The dispatch prompt is fixed text kept in one tracked file. It
      contains no task content, so the subagent reads its task from
      the repo
- [x] RULES.md states that a dispatching session dispatches at most one
      Plan task per instruction from the human, and does not itself
      edit files the subagent's task covers
- [x] A dispatched session's Session log entry records the dispatch in
      the existing Agent/tool field (mechanism and subagent model)
- [x] RULES.md states that a feature spec's Done-when may be ticked
      only after its Session log holds a review entry. That entry's
      Agent/tool line names a model that appears on no implementing
      session's Agent/tool line
- [x] RULES.md states that the human may tick without a review after
      appending a one-line waiver, with its reason, to the Session log
- [x] RULES.md states that the review gate does not apply to hotfix
      specs
- [x] AGENTS.md defines the reviewer role. A reviewer appends one log
      entry with a met / not met / cannot tell verdict per Done-when
      item, each with its evidence. It edits no other file and ticks
      nothing
- [x] A scratch spec in a throwaway repo has been taken through one
      dispatched task and one cross-model review entry. The entries
      are present in its log

## Non-goals            <!-- CONTRACT -->
- A reviewer verdict replacing the human's tick. The review is a
  precondition for acceptance, not acceptance.
- Unattended chaining of tasks: an orchestrator that runs a whole
  Plan without the human between tasks.
- A review gate on hotfix specs.
- Vendor-specific invocation in the template's tracked files, beyond
  one-line adapter files.
- Restructuring the rule files (v2-structure).
- Scribe rules, or the shape of Session log fields (v2-scribe-and-logs).
  This spec uses the existing Agent/tool field and adds none.
- Changes to the drill or to certification, including running the
  drill through a subagent (v2-commissioning).
- Application code.

## Constraints          <!-- CONTRACT -->
- Files in scope: RULES.md, AGENTS.md, NOTES.md (rationale), README.md
  ("Pointing an agent at the workflow").
- AGENTS.md edits go through the Scribe section, since
  v2-scribe-and-logs lands first.
- Lands after v2-structure and v2-scribe-and-logs, and before run 2.
- Markdown only in the template. The scratch-spec trial runs in a
  throwaway, and its evidence stays outside the template.

## Plan                 <!-- human edits; agents propose via log -->
- [x] task 1 — RULES.md and AGENTS.md: definition of a fresh session,
      the fixed dispatch prompt, and the one-task-per-instruction
      limit on dispatchers
- [x] task 2 — reviewer role in AGENTS.md; the review-before-tick gate,
      the waiver and the hotfix exemption in RULES.md's closing rule;
      the rationale in NOTES.md
- [x] task 3 — trial in a throwaway: one dispatched task and one
      cross-model review against a scratch spec. Report in this log

## Session log          <!-- agents append; human may annotate -->
### 2026-10-05 — session 1 (drafting)
Agent/tool: Claude Code (Opus 5.5)
Did: drafted this spec from the human's brief, with Status: draft. No
other file changed by this spec.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): conflicts with v1, flagged rather than resolved.
1. Principle 3 ("agents communicate only through the repo; no paste
   between a planner chat and an implementer chat"). A dispatch prompt
   is a message from one agent to another outside the repo. Done-when
   item 2 confines it to fixed, content-free text, which keeps the
   repo the only channel for task content. Say if the brief meant
   richer handoffs. Those would contradict Principle 3.
2. Principle 1 and AGENTS.md workflow item 4 ("one task per session;
   do not start the next task uninvited"). A dispatcher that lives
   across tasks is a durable non-human process. Done-when item 3 keeps
   v1's force: one dispatch per human instruction. If the brief meant
   autonomous chaining, that is a v1 rule change and needs saying.
3. LM-agnosticism and §2's one-line adapters. Subagent dispatch is a
   vendor feature, and its invocation has nowhere to live under
   one-line adapters. As drafted, RULES.md defines the property (a
   clean context, fixed prompt) and no mechanism, and a tool without
   subagents uses a new session.
4. Acceptance under v1 is purely the human's. A gate before the tick
   constrains the human, and it requires a second model family for
   every spec, always. What happens when none is available: does the
   spec wait, or may the human waive the gate with a log line?
5. Hotfix specs. The brief does not say whether the gate applies to
   them. As drafted, it covers feature specs only, since v1 keeps
   hotfix approval deliberately cheap (§6.3).
6. "Cross-model". I took it to mean a different model family as named
   on the Agent/tool line, not merely a different version or product.
   A different family is a stricter bar than §9's "the same agent in
   two different products".
7. The reviewer is a new kind of session. AGENTS.md's workflow assumes
   every session implements a Plan task. A reviewer has no task, so
   AGENTS.md needs the role defined (Done-when item 6).
8. §10. Adopting subagent dispatch is an agent-tool change, which
   triggers a drill under v1. Whether a dispatched subagent can be
   tested blind is v2-commissioning's question, and is fenced out
   here.

### 2026-10-05 — session 2 (drafting, decisions applied)
Agent/tool: Claude Code (Opus 5.5)
Did: wrote the human's answers to session 1's proposals into the
draft; Status stays draft. Decisions, in the human's chosen options:
1. "Fixed, content-free": no change; the draft already said so.
2. "One per instruction": no change; the draft already said so.
3. "Property only": Done-when item 1 now says RULES.md names no
   vendor's mechanism.
4. "Human may waive, logged": new Done-when item 6.
5. "Feature specs only": new Done-when item 7 and a Non-goal.
6. "Different model", not a different family: Done-when item 5 now
   requires a model that appears on no implementing Agent/tool line.
   Note for the reader: under that wording, Opus reviewed by Sonnet,
   or by another Opus version, passes.
7. No question needed: the draft already covered it.
8. No question needed: fenced out.
Also: since scribe-and-logs now lands first, the Constraints route
AGENTS.md edits through its Scribe section, and set this spec to land
before run 2.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): none open.

### 2026-10-07 — session 3
Agent/tool: Claude Code (Opus 5.5)
Did: task 1 — RULES.md gains "Sessions and dispatch" (fresh session as a new session or a clean-context subagent given only the dispatch prompt, no vendor mechanism named; one Plan task per human instruction; dispatcher edits none of the task's files); scribe commit first: AGENTS.md gains a Dispatch section holding the fixed, content-free dispatch prompt, and the completion rule has a dispatched session's Agent/tool line name the mechanism and its model (Done-when item 4, named by no task, placed here as dispatch work) (authorised: "i authorise that change").
Checks run: `git diff` (RULES.md, this spec only; AGENTS.md in the preceding scribe commit); `grep -n -i "dispatch" RULES.md AGENTS.md`; Commands block unset, markdown-only repo, no test applies to governance prose.
Left: tasks 2 and 3; README.md "Pointing an agent at the workflow" is in scope but not named by task 1, so it is unchanged.
PROPOSAL (if any): none.

### 2026-10-07 — session 4
Agent/tool: Claude Code (Opus 5.5)
Did: task 2 — RULES.md "Closing a spec" gains the review gate (feature specs tick Done-when only after a review entry from a model on no implementing Agent/tool line, or a one-line logged waiver with reason; hotfix specs exempt); NOTES.md gains rationale for dispatch and for the review gate; scribe commit first: AGENTS.md gains a Reviewer section (authorised: "i authorise you to scribe").
Checks run: `git diff` (RULES.md, NOTES.md, this spec; AGENTS.md in the preceding scribe commit); `grep -n -i -E "review|waiver|hotfix specs" RULES.md AGENTS.md`; Commands block unset, markdown-only repo, no test applies to governance prose.
Left: task 3; README.md "Pointing an agent at the workflow" still unchanged, named by no task.
PROPOSAL (if any): none. Noted for the human: the Reviewer section's per-item verdict lines under Did, and its "<spec-name>: review" commit message, are exceptions to the one-line log format and the Git rules' commit kinds, both shown and authorised before writing.

### 2026-10-07 — session 5
Agent/tool: Claude Code (Opus 5.5)
Did: task 3 — report on the trial the human ran in the throwaway haymanjoyce/scratch (made from this template at de5539a; RULES.md, NOTES.md, README.md identical, AGENTS.md identical but for its filled Commands block) against scratch spec scratch-upper. Dispatch: both Plan tasks (commits 2df17ee, b51d0a2) were done by sessions whose Agent/tool line reads "Grok Build subagent, dispatched with the AGENTS.md dispatch prompt (model: Grok)", one task each. Review: commit 2925603 "scratch-upper: review" adds only the review entry; its Agent/tool line is Codex (GPT-6), a model on no implementing line; it gives one verdict with evidence per Done-when item: met, met, cannot tell. The "cannot tell" is the unittest item: the reviewer ran it in PowerShell, where `python` was unavailable, rather than translating to the Commands block's bash as AGENTS.md's Commands section directs. I reran it in Git Bash: 2 tests, OK. The human then ticked all three boxes (5034d71), which the gate permits, since the review is a precondition, not acceptance.
Checks run: in scratch, `PYTHONDONTWRITEBYTECODE=1 python -m unittest discover -s tests` (Git Bash; Ran 2 tests, OK); `git log` and `git show` on the scratch commits above; `diff` of scratch's rule files against this repo's. Here: Commands block unset, markdown-only repo, no test applies to a trial report.
Left: Done-when for the human, after the review gate. Observations from the trial, none a v2-agents fault: (1) the repo holds only the dispatched sessions' own claims that the prompt was verbatim and the context clean, and no entry from the dispatching session; (2) scratch-upper's closure is partial: Status is done, but the file is not in specs/done/ and _active.md still names it; (3) the closing commit tracked tests/__pycache__/*.pyc, as the template's .gitignore leaves language ignores to commissioning; (4) a throwaway made from this template carries this repo's own specs (v2-agents, v2-commissioning, specs/done/*), which concerns v2-commissioning.
PROPOSAL (if any): none.

### 2026-10-07 — session 6 (log note)
Agent/tool: Claude Code (Opus 5.5)
Did: noted, at the human's request, that scratch commit fbea2d0 moved scratch-upper to specs/done/ and set _active.md to none, which settles observation (2) in session 5; observation (3) still stands, the .pyc is still tracked.
Checks run: in scratch, `git show --stat fbea2d0`, `cat specs/_active.md`, `git ls-files tests`.
Left: Done-when for the human, after the review gate.
PROPOSAL (if any): none.
