# Spec: v2-commissioning

Status: approved
Created: 2026-10-05

## Goal
Each template version is proven once by one full dummy-dev loop, run
with any one agent product. Each agent product is then certified for
that version by one scripted fire drill. Both results are recorded in
the template's assurance log. One certified product is enough: v1's
two-product bar is dropped. A project made from a certified template
version, and worked by a product certified for it, inherits that
certification. It runs the drill once before real work, instead of
full commissioning. The drill replaces refusal tests A–D as four
hand-run sessions. It is one script, run by the conductor, that stages
each test's repo state, runs each test in a fresh session, judges the
result and prints one pass/fail line. A manual version of the same
four tests exists for products the script cannot drive yet.

## Done when            <!-- CONTRACT — human edits, human ticks -->
- [ ] RULES.md carries the template's version identifier, and
      docs/commissioning.md lists the changes that require a new
      version
- [ ] docs/commissioning.md defines the full loop: one dummy feature
      taken from draft through approval, task-by-task implementation
      and acceptance to close, with v1 §9 step 5's checks on each task
      (stops after one task, ticks only the Plan box, wrote a test,
      logged, committed once)
- [ ] docs/commissioning.md states that a (version, product) pair is
      certified when the version has a passing full-loop row, run with
      any product, and that product has a passing drill row. No
      tracked file outside specs/done/ requires two products
- [ ] docs/assurance-log.md has two tables. "Template certification"
      holds rows with template version, kind (loop or drill), agent
      product, date, drill script commit hash (drill rows) and result.
      "Project drills" holds the child project's own drill lines. A
      child appends only to "Project drills"
- [ ] docs/commissioning.md states that a child project records the
      template version it was made from. Inheritance holds only for
      that version, a product certified for it, and an AGENTS.md that
      differs from the template's in the Commands block alone.
      Otherwise the child runs the full loop and the drill itself
- [ ] docs/commissioning.md states that an inheriting child runs the
      drill once, and logs the result, before its first real feature
      spec is approved
- [ ] The drill runs as one command. Each test runs in its own fresh
      session. It prints exactly one line of the form
      `DRILL <date> template=<v> agent=<product> A=<pass|fail>
      B=<pass|fail> C=<pass|fail> D=<pass|fail> result=<pass|fail>`
- [ ] The drill judges each test from repo state after the session
      (files and sections changed or unchanged), not from the session's
      reply. A run against a stub agent that edits files regardless
      prints fail for all four tests
- [ ] docs/commissioning.md gives the four tests as manual steps that
      produce a line in the same format
- [ ] The drill script, and anything encoding its pass criteria, is
      absent from the template's tracked tree (`git ls-files`)
- [ ] The certification table holds a passing full-loop row and a
      drill row, produced by the script, for the current template
      version

## Non-goals            <!-- CONTRACT -->
- Changing the rules the drill probes. The drill tests the draft gate,
  the "none" gate, the contract-edit line and the Plan-edit line as
  they stand in the version being certified, scribe rule included. The
  scribe rule itself belongs to v2-scribe-and-logs.
- Splitting or restructuring the rule files (v2-structure). This spec
  edits docs/commissioning.md and RULES.md as v2-structure leaves
  them.
- Subagent dispatch, or a reviewer gate on acceptance (v2-agents).
- Running the drill or the loop in CI, on a schedule, or anywhere else
  unattended. The conductor runs them.
- Scripting the full loop. It stays a conductor-run procedure.
- Pushing, tagging or publishing a template release automatically.
- Application code in the template.

## Constraints          <!-- CONTRACT -->
- Files in scope (template repo): docs/commissioning.md, RULES.md
  (version line, pointer only), NOTES.md (rationale),
  docs/assurance-log.md, README.md ("Starting a new project", "Keeping
  it honest").
- The drill script lives outside every repo made from the template:
  in the commissioning evidence repo, or another location that is not
  a template copy. Certification rows cite it by commit hash.
- The script reaches agents only through a per-product adapter (the
  command that starts a fresh, non-interactive session). Adapters live
  with the script, not in the template.
- Lands last of the four v2 specs. Its final Done-when item is run 2:
  the first certification of the finished v2 template.

## Plan                 <!-- human edits; agents propose via log -->
- [x] task 1 — docs/commissioning.md: version bump rule; the full loop;
      the certification bar (one product); inheritance conditions; the
      child's drill replacing full commissioning; the manual drill.
      RULES.md: version line and pointer. Rationale to NOTES.md
- [ ] task 2 — docs/assurance-log.md: "Template certification" and
      "Project drills" tables, with columns matching the drill line
- [ ] task 3 — the drill script, outside the template: stage A, D, B
      and C in a throwaway made from the template, one fresh session
      each, judge from git state, print the line. One product adapter
- [ ] task 4 — negative control against a stub agent (all fail)
- [ ] task 5 — run 2: the full loop and one scripted drill against the
      current version. Record both rows in the certification table

## Session log          <!-- agents append; human may annotate -->
### 2026-10-05 — session 1 (drafting)
Agent/tool: Claude Code (Opus 5.5)
Did: drafted this spec from the human's brief, with Status: draft. No
other file changed by this spec.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): conflicts with v1, flagged rather than resolved.
1. The blind-test rule (§9, "where commissioning notes may live"). A
   script that judges pass/fail encodes each test's expected outcome.
   Kept in the template, it would ship into every child, which is
   exactly what §9 forbids. The Constraints put it outside, but then
   "certified at template level" depends on an artefact the template
   does not contain. Suggest the certification row records the
   script's commit hash, so the record stays checkable.
2. LM-agnosticism and §2's "no tooling at day zero". A conductor
   script has to start sessions in a specific vendor's CLI. The
   per-product adapter keeps vendor detail out of the template, but
   the drill is no longer something any human can run by hand from
   the text alone. Keep a manual fallback in NOTES.md?
3. The two-product bar (§9's closing rule, §13). The brief certifies
   per (version, product). v1 says the loop is real only after two
   different products. Options: (a) a pair is certified by one pass,
   and the template version counts as commissioned once two products
   are certified for it; (b) drop the two-product bar. Done-when item
   2 leaves "what makes a pair certified" for RULES.md to state.
   Choose before approval.
4. What template-level certification consists of. The brief collapses
   A–D into a drill but does not say whether certifying a template
   version still runs the full dummy-dev loop of §9 (one feature,
   end to end) or only the drill. I assumed the full loop stays for
   certification and children get the drill alone. Confirm.
5. No version is currently certified. Run 1 tested the template
   before template-hardening, and the four v2 specs change it again.
   Run 2, the standing next step, would certify whichever version it
   runs against. Under v1's procedure or this one?
6. Inherited log rows. "Use this template" copies
   docs/assurance-log.md, so the child receives the template's
   certification rows. That is the inheritance mechanism, but the
   rows then sit in a file the child also appends its own drills to.
   Task 2's two tables address this. Say if the certification record
   should be a separate file instead.
7. §10's "each drill is one fresh session" becomes four sessions per
   drill. Its "two consecutive failures" rule carries over per test
   letter.
8. Interaction with v2-scribe-and-logs. Judging from git state copes
   with either rule set. The script never authorises a change, so
   under a scribe rule a pass on C or D is still "contract or Plan
   unchanged".

### 2026-10-05 — session 2 (drafting, decisions applied)
Agent/tool: Claude Code (Opus 5.5)
Did: wrote the human's answers to session 1's proposals into the
draft; Status stays draft. Decisions, in the human's chosen options:
1. "Commit hash in the row": in the Constraints and Done-when item 4.
2. "Yes, in the human-only file": the manual drill goes in
   docs/commissioning.md (v2-structure Q2), not NOTES.md. Done-when
   item 9.
3. "Drop the two-product bar": one product certifies. Done-when item 3
   removes the bar from every tracked file outside specs/done/. That
   reverses v1 §9's closing rule and §13's checklist item, which
   template-hardening task 6 had made explicit.
4. Asked as "drill only"; the human then said "keep one full loop per
   version". So certification is one full loop per version, with any
   product, plus one drill per product (Goal, Done-when items 2, 3 and
   11). The loop stays conductor-run, not scripted (Non-goal).
5. "After all four v2 specs": run 2 is task 5 and the last Done-when
   item, under this spec's procedure.
6. "Two tables, one file": Done-when item 4.
7. No question needed: carried as stated.
8. No question needed: the Non-goals now say the drill tests the
   scribe-era rules.
The rules moved from RULES.md to docs/commissioning.md, following
v2-structure's decision that these procedures are human-only.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): none open.

### 2026-10-07 — session 3
Agent/tool: Claude Code (Opus 5.5)
Did: task 1 — docs/commissioning.md rewritten: Template versions (bump list), Certification (one product; loop row any product + drill row per product; drill rows cite script hash; notes-location rule extended to the script), Starting a project from the template (version recorded by the copied RULES.md line; three inheritance conditions; inheriting child drills once before first real spec approval, else full loop + drill), Full loop (refusal tests removed; step-5 checks on every task; closes via review gate), Fire drill (scripted line format; manual A, D, B, C steps judged from git state), Build checklist (two-product item replaced by one certified pair); RULES.md version line set to "Template version: 2" with pointer, and the commissioning pointer now covers inheritance; NOTES.md gains two rationale sections.
Checks run: `git diff` (RULES.md, NOTES.md, docs/commissioning.md, this spec); `grep -rniE "two (different )?(agents|products)|twice" --exclude-dir=.git --exclude-dir=done .` (only hits: this spec and NOTES.md's history of v1); Commands block unset, markdown-only repo, no test applies to governance prose.
Left: tasks 2–5; README.md "Starting a new project" and "Keeping it honest" are in scope but named by no task, so unchanged (the latter still says "one fresh session").
PROPOSAL (if any): none. Noted for the human: (1) version numbered "2", whole numbers, a choice of mine — the spec names no format; (2) a non-inheriting child's own full-loop result has no named table (Done-when 4 gives "Project drills" drill lines only) — task 2 may need a decision; (3) the manual drill states pass criteria in this tracked file, as v1 did; Done-when item 10 is read as covering the script's criteria only.

### 2026-10-08 — session 4
Agent/tool: Claude Code (Opus 5.5)
Did: follow-up to task 1, the human's answer to session 3's note 1 ("format is 2.0"): RULES.md version line set to "Template version: 2.0"; docs/commissioning.md bump rule now "the next whole number (2.0, then 3.0)". Notes 3 and 4 answered "ok".
Checks run: `git diff` (RULES.md, docs/commissioning.md, this spec); Commands block unset, markdown-only repo, no test applies to governance prose.
Left: tasks 2–5; session 3's note 2 (where a non-inheriting child records its own full loop) awaits the human.
PROPOSAL (if any): none.
