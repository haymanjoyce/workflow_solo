# Spec: v2-agents

Status: approved
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
- [ ] RULES.md defines a fresh session as either a new session or a
      subagent whose context holds none of the dispatching session's
      conversation, given only the fixed dispatch prompt. It names no
      vendor's mechanism
- [ ] The dispatch prompt is fixed text kept in one tracked file. It
      contains no task content, so the subagent reads its task from
      the repo
- [ ] RULES.md states that a dispatching session dispatches at most one
      Plan task per instruction from the human, and does not itself
      edit files the subagent's task covers
- [ ] A dispatched session's Session log entry records the dispatch in
      the existing Agent/tool field (mechanism and subagent model)
- [ ] RULES.md states that a feature spec's Done-when may be ticked
      only after its Session log holds a review entry. That entry's
      Agent/tool line names a model that appears on no implementing
      session's Agent/tool line
- [ ] RULES.md states that the human may tick without a review after
      appending a one-line waiver, with its reason, to the Session log
- [ ] RULES.md states that the review gate does not apply to hotfix
      specs
- [ ] AGENTS.md defines the reviewer role. A reviewer appends one log
      entry with a met / not met / cannot tell verdict per Done-when
      item, each with its evidence. It edits no other file and ticks
      nothing
- [ ] A scratch spec in a throwaway repo has been taken through one
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
- [ ] task 3 — trial in a throwaway: one dispatched task and one
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
