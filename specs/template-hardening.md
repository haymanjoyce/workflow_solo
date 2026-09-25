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
      and §9.9 confirms that block rather than filling it
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
- [ ] task 1 — §9: move Commands to step 2; reword §9.9 to confirm
- [ ] task 2 — §9: add the rule on where commissioning notes may live
- [ ] task 3 — add refusal test D to §9 between steps 4 and 5, extend
      §10's drill and docs/assurance-log.md's columns from A–C to A–D
- [ ] task 4 — reconcile §5's required log content with TEMPLATE.md's
      Agent/tool field (AGENTS.md + §7 fenced copy)
- [ ] task 5 — add a shell convention to the Commands block
      (AGENTS.md + §7 fenced copy)
- [ ] task 6 — §13: make the two-product bar explicit in the item
- [ ] task 7 — §2: add tests/ to the skeleton

## Session log          <!-- agents append; human may annotate -->
