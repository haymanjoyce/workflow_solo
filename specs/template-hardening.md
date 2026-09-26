# Spec: template-hardening

Status: approved
Created: 2026-09-25

## Goal
Apply the seven findings from the first commissioning run to the
template itself, so that the second-product commissioning pass tests a
template whose own procedure is self-consistent. Today §9 tells the
operator to fill the Commands block last while §5 requires it from the
first task; it is silent on where commissioning notes may live, which
cost run 1 its blind results on tests A and B; and §13's checklist can
be ticked after one agent product when §9 requires two.

## Done when            <!-- CONTRACT — human edits, human ticks -->
- [ ] §9 fills the Commands block before the first implementation step,
      and §9's final step confirms that block rather than filling it
- [ ] §9 states where commissioning notes may live, and lists refusal
      test D at a position before human acceptance
- [ ] §13's commissioning item names the two-product bar in its own text
- [ ] AGENTS.md's Commands block states the shell its values assume,
      and §5's required log content matches specs/TEMPLATE.md's fields
- [ ] §2's skeleton includes tests/
- [ ] AGENTS.md and WORKFLOW.md §7's fenced copy are byte-identical

## Non-goals            <!-- CONTRACT -->
- Any change to the four rules the refusal tests probe: the draft-status
  gate, the "_active: none" gate, the contract-edit line, the Plan-edit
  line. Run 1's behavioural evidence must stay valid.
- Any commissioning evidence added to this repo's tracked tree.
- Re-running commissioning. That is the second-product pass, after this.
- Application code. src/ stays empty.

## Constraints          <!-- CONTRACT -->
- Files in scope: WORKFLOW.md, AGENTS.md, specs/TEMPLATE.md,
  docs/assurance-log.md.
- WORKFLOW.md §7 contains a fenced copy of AGENTS.md that commissioning
  §13 diffs verbatim. Any task touching AGENTS.md must change both, in
  the same commit, or the next run's Phase 0.3 fails.
- AGENTS.md is human-edit-only. Tasks 4 and 5 need either the human's
  hand or an explicit per-session scribe authorisation, recorded.
- Markdown only. No dependencies, no tooling, no new files outside those
  listed above.

## Plan                 <!-- human edits; agents propose via log -->
- [x] task 1 — §9: move Commands to step 2; reword §9.9 to confirm
- [ ] task 2 — §9: add the rule on where commissioning notes may live
- [ ] task 3 — add refusal test D to §9 immediately after the first
      implementation session and before the remaining ones (spec active
      and approved, before acceptance), extend §10's drill and
      docs/assurance-log.md's columns from A–C to A–D
- [ ] task 4 — reconcile §5's required log content with TEMPLATE.md's
      Agent/tool field (AGENTS.md + §7 fenced copy)
- [ ] task 5 — add a shell convention to the Commands block
      (AGENTS.md + §7 fenced copy)
- [ ] task 6 — §13: make the two-product bar explicit in the item
- [ ] task 7 — §2: add tests/ to the skeleton

## Session log          <!-- agents append; human may annotate -->
### 2026-09-25 — session 1
Agent/tool: Claude Code (Opus 5)
Did: task 1. WORKFLOW.md §9 only. Filling the AGENTS.md Commands block
is now step 2, before any implementation step, with a one-line reason
(§5 makes an empty block unverifiable from the first task) and a note
that a provisional value is fine. The old step 9 is now step 10 and
confirms the block against what commissioning ran rather than filling
it. Steps 2–8 of the old list shifted down one; no other file changed.
Checks run: none — AGENTS.md's Commands block is empty (install/test/
lint unset) in this markdown-only repo, so there is nothing to run.
No test written: the change is prose in a specification document with
no executable behaviour (§5's docs-only case). Verified by reading:
§9's step numbering is contiguous 1–10, and no other text in the repo
cites a §9 step number (grep for "§9" and "step N" — only §10 and §13
reference §9, both by test letter, which task 3 updates).
Left: tasks 2–7. Note for the human, not a plan change: this task's
insertion renumbers §9's final item from 9 to 10, so the Done-when
line reading "§9.9 confirms that block" now points at §9.10. The Plan
task's wording ("move Commands to step 2") was followed literally.
Task 3's "between steps 4 and 5" reads, under the new numbering, as
between refusal test A and the first implementation session.
PROPOSAL (if any): none.
