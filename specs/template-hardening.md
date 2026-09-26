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
- [x] task 2 — §9: add the rule on where commissioning notes may live
- [x] task 3 — add refusal test D to §9 immediately after the first
      implementation session and before the remaining ones (spec active
      and approved, before acceptance), extend §10's drill and
      docs/assurance-log.md's columns from A–C to A–D
- [x] task 4 — reconcile §5's required log content with TEMPLATE.md's
      Agent/tool field (AGENTS.md + §7 fenced copy)
- [x] task 5 — add a shell convention to the Commands block
      (AGENTS.md + §7 fenced copy)
- [x] task 6 — §13: make the two-product bar explicit in the item
- [x] task 7 — §2: add tests/ to the skeleton

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

### 2026-09-26 — session 2
Agent/tool: Claude Code (Opus 5)
Did: task 2. WORKFLOW.md §9 only. Added a bolded rule, "Where
commissioning notes may live", between the suggested-dummy line and
step 1, so the operator reads it before doing anything. It requires the
commissioning plan, each refusal test's expected outcome, and the run
record to live outside the repo under test — excluding untracked files
in the working copy as well as the tracked tree, since an agent reads
whatever is in the repo it is pointed at — and states the reason (a
session that knows it is being tested gives no blind result). It names
the one commissioning output that does belong in the repo: the
`docs/assurance-log.md` entry of §10, written after the run.
Checks run: none — AGENTS.md's Commands block is empty (install/test/
lint unset) in this markdown-only repo, so there is nothing to run.
No test written: prose in a specification document, no executable
behaviour (§5's docs-only case). Verified by reading: the rule sits
before step 1 so §9's steps are untouched and still numbered 1–10; it
refers to "the refusal tests" without a letter range, so task 3's
addition of test D does not leave it stale; §7's fenced AGENTS.md copy
was not touched, so it stays byte-identical to AGENTS.md.
Left: tasks 3–7. Task 3 is next and extends §9, §10 and
docs/assurance-log.md from A–C to A–D.
PROPOSAL (if any): none.

### 2026-09-26 — session 3
Agent/tool: Claude Code (Opus 5)
Did: task 3. WORKFLOW.md and docs/assurance-log.md.
- §9: new step 6, "Refusal test D (plan)" — a fresh session is asked to
  drop or add a Plan task and must refuse, recording a "PROPOSAL:" in
  the Session log instead. It sits immediately after the first
  implementation session and before the remaining ones, with the spec
  active, approved and part-implemented; the step states why that
  position is required (after acceptance `_active.md` is `none`, so
  test B's gate would explain any refusal and D would prove nothing).
  Old steps 6–10 are now 7–11.
- §9 step 2: the forward reference to the Commands confirmation now
  reads "the final step" instead of "step 10", which this insertion
  would otherwise have made wrong. Content-anchored, so later
  insertions cannot break it again.
- §10: drill range A–C → A–D, log columns A/B/C → A/B/C/D, plus one
  clause that D needs a spec that is active, approved and has an
  unticked Plan task — run the drill while one is in play or stand up
  a scratch spec.
- docs/assurance-log.md: added the "D (plan)" column to the header and
  separator. No rows exist yet.
- §13: the checklist item's "refusal tests A–C passed" → "A–D". Not
  named in the Plan task, but this task is what made it stale, and
  task 6 rewrites the same line for the two-product bar — revert it
  there if you would rather that task own the whole line.
Checks run: none — AGENTS.md's Commands block is empty (install/test/
lint unset) in this markdown-only repo, so there is nothing to run.
No test written: prose and a table header in documents, no executable
behaviour (§5's docs-only case). Verified by reading: §9's steps are
contiguous 1–11; `diff` of AGENTS.md against §7's fenced copy reports
no difference (neither was touched); grep for "A–C", "A/B/C", "§9" and
"step N" across the repo leaves only the README hits below.
Left: tasks 4–7, and README.md lines 29 and 31, which still say "A–C"
and "A/B/C" — see the proposal.
PROPOSAL (if any): README.md paraphrases §10's drill rule and now
disagrees with it (it still says A–C / A/B/C). README.md is not in this
spec's Constraints "files in scope", so I did not touch it. Suggest
adding README.md to that list and a "task 8 — README: update the drill
paraphrase to A–D". Alternatively, drop the letters from README and
point at §10, so the paraphrase cannot drift again.

### 2026-09-26 — session 4
Agent/tool: Claude Code (Opus 5)
Scribe authorisation: the human was shown both hunks before anything
was written and answered "Authorise me as scribe" to the question
"AGENTS.md is human-edit-only. How should the AGENTS.md hunk of task 4
be applied?", granting an explicit per-session scribe authorisation for
AGENTS.md. Recorded here per this spec's Constraints.
Did: task 4. WORKFLOW.md and AGENTS.md. specs/TEMPLATE.md's log block
has five fields (Agent/tool, Did, Checks run, Left, PROPOSAL) but §5.3
and AGENTS.md's completion rule both listed four — agent/tool was
required by the template and by nothing else. Reconciled towards the
template, so TEMPLATE.md itself is unchanged:
- WORKFLOW.md §5 item 3 now requires every field of TEMPLATE.md's log
  block, named in the template's order, with one line on why the
  agent/tool field earns its place (attribution of a result to a
  model, which §10's drill reads).
- AGENTS.md's final "Completing a task" bullet now names the same five
  fields and points at specs/TEMPLATE.md as their source, so the two
  documents cannot drift apart field-by-field again.
- §7's fenced copy took the identical AGENTS.md hunk, same commit, per
  this spec's Constraints.
Checks run: none — AGENTS.md's Commands block is empty (install/test/
lint unset) in this markdown-only repo, so there is nothing to run.
No test written: prose in governance documents, no executable
behaviour (§5's docs-only case). Verified by reading: `diff` of
AGENTS.md against §7's fenced copy extracted from WORKFLOW.md reports
no difference; the five field names in §5, in AGENTS.md and in
TEMPLATE.md's block now agree in both content and order.
Left: tasks 5–7, and the README drift raised in session 3, still open.
Task 5 also edits AGENTS.md (the Commands block) and will need its own
scribe authorisation — this one was for this session only.
PROPOSAL (if any): none.

### 2026-09-26 — session 5
Agent/tool: Claude Code (Opus 5)
Scribe authorisation: the human was shown the hunk before anything was
written and answered "Authorise me as scribe" to the question "Task 5
adds a shell convention to AGENTS.md's Commands block. Apply it how?",
granting an explicit per-session scribe authorisation for AGENTS.md.
Recorded here per this spec's Constraints. Separate from session 4's,
which covered task 4 only.
Did: task 5. AGENTS.md and WORKFLOW.md.
- AGENTS.md's Commands block gains a "shell:" field above install/
  test/lint, and its parenthetical now says what that field is for:
  the same command line can fail, or mean something else, in another
  shell. It also states what to do when a session's shell differs —
  translate and say so in the log, never substitute a different
  command and record it as the check, which would make §5's tick
  describe something commissioning never ran.
- §7's fenced copy took the identical hunk, same commit, per this
  spec's Constraints.
- §9 step 2's parenthetical list "(install / test / lint)" is now
  "(shell / install / test / lint)". Not named in the Plan task, but
  this task is what made it incomplete.
Deviation from the approved hunk, for the record: the approved preview
wrote the field as `shell:` in backticks. AGENTS.md uses no backticks
anywhere, so it went in as "The shell line names the shell these lines
are written for". Same rule, file's own idiom; say the word if you
want the backticks.
Checks run: none — AGENTS.md's Commands block still has no values
(shell/install/test/lint unset) in this markdown-only repo, so there
is nothing to run. Adding the field does not change that; the block is
filled per §9 step 2 by whoever commissions a real project from this
template.
No test written: prose in governance documents, no executable
behaviour (§5's docs-only case). Verified by reading: `diff` of
AGENTS.md against §7's fenced copy extracted from WORKFLOW.md reports
no difference; grep for "install / test / lint" and "Commands block"
across the repo leaves no stale list.
Left: tasks 6 and 7, and the README drift raised in session 3, still
open. Task 6 (§13's two-product bar) and task 7 (§2's skeleton) touch
WORKFLOW.md only, so neither needs a scribe authorisation.
PROPOSAL (if any): none.

### 2026-09-26 — session 6
Agent/tool: Claude Code (Opus 5)
Did: task 6. WORKFLOW.md §13 only. The commissioning checklist item
now carries the two-product bar in its own text: commissioning is
"completed **twice** — the whole loop ... run through by two different
agents (or the same agent in two different products), per §9's closing
rule. One pass is half the bar: do not tick this on one". Before, the
item said only that §9 was completed, so it read as tickable after a
single pass while §9's closing line required two; a reader who ticked
from the checklist alone never met §9. The parenthetical is worded
verbatim from §9's closing line so the two cannot be read as different
bars. No other file changed; the item stays unticked.
Checks run: none — AGENTS.md's Commands block has no values
(shell/install/test/lint unset) in this markdown-only repo, so there
is nothing to run.
No test written: prose in a specification document, no executable
behaviour (§5's docs-only case). Verified by reading: §13's remaining
items are unchanged and the item's "two different agents (or the same
agent in two different products)" matches §9's closing line word for
word (grep "two different agents" returns exactly those two places).
Left: task 7, and the README drift raised in session 3, still open.
Also noted, not changed: §13's next item still says
`docs/assurance-log.md` is created "with the commissioning drill as
entry one". Two commissioning passes produce two entries. The line is
not wrong — the first pass is still entry one — so I left it; say if
you want it to read "an entry per pass".
PROPOSAL (if any): none.

### 2026-09-26 — session 7
Agent/tool: Claude Code (Opus 5)
Did: task 7, the last Plan task. WORKFLOW.md only.
- §2's day-zero skeleton gains `tests/` below `src/`, commented
  "likewise; §5 requires a test per task" — §5 makes a test the
  condition of every tick and §4's matrix already grants agents edit
  rights over tests, so the directory was assumed everywhere but
  never listed.
- §13's first checklist item now reads "`src/` and `tests/` empty",
  since the skeleton it checks has two empty directories now. Not
  named in the Plan task; this task is what made the item partial.
Checks run: none — AGENTS.md's Commands block has no values
(shell/install/test/lint unset) in this markdown-only repo, so there
is nothing to run.
No test written: prose in a specification document, no executable
behaviour (§5's docs-only case). Verified by reading: the skeleton's
comment column still aligns; `diff` and `cmp` of AGENTS.md against
§7's fenced copy extracted from WORKFLOW.md both report no
difference, which is Done-when item 6.
Noted, not changed: §4's matrix row reads "`src/`, tests" — correct,
but now that §2 names the directory it could read "`tests/`". Cosmetic
only, so left alone.
Left: nothing in the Plan — tasks 1–7 are all ticked. Two things are
outside it and yours to decide: (a) the README drift from session 3,
still unfixed, README.md being out of this spec's files-in-scope;
(b) this repo's own tree has no `tests/` (it uses .gitkeep for empty
directories — `src/.gitkeep`, `specs/done/.gitkeep`), so as of this
commit the template no longer satisfies its own §13 item 1. See the
proposal. Done-when is yours to tick; all six items look met to me,
but that judgement is acceptance and not mine to make.
PROPOSAL (if any): add `tests/.gitkeep` to this repo, so the template
matches the §2 skeleton it now specifies and the next commissioning
run's Phase 0 skeleton check passes. It needs a Constraints amendment
first: "Markdown only ... no new files outside those listed above"
excludes it, and .gitkeep is not markdown. Suggest amending
Constraints to allow it plus a "task 8 — add tests/.gitkeep", or
folding it into the same task 8 as the README fix.
