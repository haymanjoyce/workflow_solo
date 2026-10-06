# Spec: v2-scribe-and-logs

Status: done
Created: 2026-10-05

## Goal
The human can change a spec's contract, its Plan, its Status,
specs/_active.md, docs/product.md or AGENTS.md by giving an agent the
change in their own words. The agent applies and commits it under a
standing scribe rule in AGENTS.md, so no spec has to invent the
convention in its Constraints the way template-hardening did. The same
rule lets an agent draft a new spec, contract sections included, at
the human's request; nothing in it is contract until the human
approves it. The decision stays the human's; only the typing moves. Every Session log entry has v1's five fields, one line each, so
a reader can scan it in seconds. Prose appears only where a session
deviated from its task or is proposing a change.

## Done when            <!-- CONTRACT — human edits, human ticks -->
- [x] AGENTS.md has a Scribe section, and `grep -rn -i scribe` outside
      specs/done/ finds the rule there
- [x] The Scribe section lists the artefacts a scribe may change:
      a spec's Goal, Done-when text, Non-goals, Constraints, Plan and
      Status; specs/_active.md; docs/product.md; AGENTS.md. Ticking
      Done-when checkboxes is not on the list
- [x] The Scribe section requires the agent to show the human the
      exact change, and to write only after an explicit authorisation
      given in reply to that shown change. It states that a request to
      make a change is never, by itself, authorisation
- [x] The Scribe section requires the human's authorising words to be
      quoted in the session's Did line
- [x] The Scribe section requires a scribe edit to be its own commit,
      separate from task work, with a message naming it as a scribe
      edit
- [x] The Scribe section states that an agent may draft a new spec,
      contract sections included, at the human's request, only with
      Status: draft
- [x] Every "never edit" or "read only" statement in AGENTS.md and
      RULES.md that covers an artefact on the scribe list names the
      Scribe section as its one exception
- [x] specs/TEMPLATE.md's log block has exactly five fields, each a
      single line: Agent/tool, Did, Checks run, Left, PROPOSAL. It says
      where deviation and proposal prose goes
- [x] AGENTS.md's completion rule and TEMPLATE.md name the same five
      fields in the same order

## Non-goals            <!-- CONTRACT -->
- Letting an agent decide a contract change, or tick Done-when. The
  human's words remain the only source of a contract change, and
  acceptance remains the human's own act.
- Restructuring the rule files (v2-structure). This spec edits
  RULES.md and AGENTS.md as v2-structure leaves them.
- Changing the refusal tests, the drill or commissioning, including
  how tests C and D are judged once a scribe rule exists
  (v2-commissioning).
- Subagent dispatch or reviewer entries in the log (v2-agents).
- Reformatting existing Session logs, including those in specs/done/.
- Application code.

## Constraints          <!-- CONTRACT -->
- Files in scope: AGENTS.md, RULES.md, specs/TEMPLATE.md,
  specs/TEMPLATE-hotfix.md (if its "as feature spec" log line needs
  it), NOTES.md (rationale only).
- Lands after v2-structure and before run 2. Run 2 certifies the
  finished v2 template, scribe rule included.
- Until this spec's task 1 is committed, no standing scribe rule
  exists. So task 1's AGENTS.md edit needs the human's hand or a
  per-session scribe authorisation, recorded, as in template-hardening
  sessions 4, 5 and 9.
- Markdown only.

## Plan                 <!-- human edits; agents propose via log -->
- [x] task 1 — AGENTS.md Scribe section: scope list, the shown-change
      and explicit-yes precondition, the quote in Did, own-commit rule,
      drafting new specs. Add exception cross-references to the "never
      edit" statements in AGENTS.md and to RULES.md's edit-authority
      matrix
- [x] task 2 — terse log format: rewrite TEMPLATE.md's log block, and
      align AGENTS.md's completion rule and TEMPLATE-hotfix.md with it

## Session log          <!-- agents append; human may annotate -->
### 2026-10-05 — session 1 (drafting)
Agent/tool: Claude Code (Opus 5.5)
Did: drafted this spec from the human's brief, with Status: draft. No
other file changed by this spec.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): conflicts with v1, flagged rather than resolved.
1. Refusal tests C and D. Test C asks a session to "just tweak the
   Goal"; test D asks it to drop a Plan task. Both are a human asking
   in their own words, which is exactly what this brief makes
   actionable. Done-when item 3, which says a request is not
   authorisation, is my attempt to keep both tests meaningful, but it
   changes what passing means: from "refuses" to "does not write
   without a shown change and explicit authorising words". The drill
   needs the same revision. That belongs to v2-commissioning and is
   fenced out of this spec. Please confirm the distinction holds, or
   define the authorising words.
2. The letter of v1. Principle 5 ("changing the contract is a human
   decision, always") survives. §4's matrix ("read only, ever") and
   AGENTS.md's "What you may never edit" do not survive as written.
   Template-hardening's Non-goals protected those lines so that run
   1's evidence stayed valid. Once this spec lands, that evidence
   covers rules that no longer stand.
3. Sequencing. Template-hardening session 10 preferred landing the
   scribe rule after run 2, so run 2 closes the two-product bar
   against the rules run 1 tested and the carve-out is then
   commissioned on its own. The brief does not say. Before or after
   run 2?
4. Where the authorisation quote goes. Five one-line fields leave no
   slot for it. Sessions 4, 5 and 9 gave it its own paragraph. Options:
   inside Did ("Did: scribe — <change>; authorised: "<words>""), or
   as permitted prose under the deviation rule. A sixth field would
   break the brief's "five".
5. docs/product.md. v1 makes it human-only, and the scribe precedent
   never touched it. The Goal leaves it off the scribe list. Say if
   it belongs on.
6. Drafting. As in v2-structure's proposal 5, v1 does not say whether
   an agent may write a new draft spec's contract sections. The Scribe
   section is the natural place to say so.
7. Field names. The brief's five fields fit v1's existing five
   (Agent/tool, Did, Checks run, Left, PROPOSAL), so I assumed no
   rename. §5 item 2's "say so explicitly" when no test applies fits
   on the Checks run line.

### 2026-10-05 — session 2 (drafting, decisions applied)
Agent/tool: Claude Code (Opus 5.5)
Did: wrote the human's answers to session 1's proposals into the
draft; Status stays draft. Decisions, in the human's chosen options:
1. "Shown change + explicit yes": Done-when item 3 now requires the
   yes to be given in reply to the shown change.
2. Accepted as a consequence: run 1's evidence covers v1 rules that
   this spec changes. Run 2 recertifies.
3. "After all four v2 specs": this spec lands before run 2. Added to
   the Constraints.
4. "Inside Did": new Done-when item 4.
5. "Yes, on the scribe list": docs/product.md added to the Goal and
   to Done-when item 2's list.
6. From v2-structure's Q5, "Cover it in the Scribe rule": new
   Done-when item 6, and the Goal.
7. "Keep v1's five": the field names are now in Done-when item 8.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): none open.

### 2026-10-06 — session 3
Agent/tool: Claude Code (Opus 5.5)
Did: task 1, under a per-session scribe authorisation per this spec's
Constraints: the human was shown the exact hunks and answered "i
authorise you". AGENTS.md gains a Scribe section (scope list, shown
change and explicit authorisation, the quote in Did, own-commit rule,
drafting with Status: draft); "What you may never edit" and "Plan
changes" name it as the one exception. RULES.md gains one line under
the edit-authority table naming the same exception for its human rows.
Task edit and scribe edit share one commit, as in template-hardening
sessions 4 and 5: the own-commit rule was not in force until this
commit.
Checks run: `grep -rn -i scribe` outside specs/done/ (finds AGENTS.md
and RULES.md). Commands block unset, markdown-only repo; no test
applies to governance prose.
Left: task 2. NOTES.md rationale for the scribe rule is in scope but
not named by task 1, so it was not added.
PROPOSAL (if any): none.

### 2026-10-06 — session 4
Agent/tool: Claude Code (Opus 5.5)
Did: task 2 — TEMPLATE.md log block gains a one-line-per-field note saying prose goes only under PROPOSAL; TEMPLATE-hotfix.md unchanged ("as feature spec" inherits it); two scribe commits first: AGENTS.md completion rule names the five fields (authorised: "i authorise you to act as scribe"), Done-when item 9 and task 2 drop RULES.md's completion rule, which v2-structure removed (authorised: "i authorise that change"); the human's tick of Done-when item 1 is included at their request.
Checks run: `sed -n '/## Session log/,$p' specs/TEMPLATE.md` and `grep -n -A2 "every field" AGENTS.md` (same five fields, same order); Commands block unset, markdown-only repo, no test applies to governance prose.
Left: NOTES.md rationale for the scribe rule and terse logs, in scope but named by no task.
PROPOSAL (if any): none.

### 2026-10-06 — session 5
Agent/tool: Claude Code (Opus 5.5)
Did: NOTES.md gains rationale sections "The scribe moves typing, not decisions" and "Terse logs", at the human's request ("add the NOTES.md rationale"); in the Constraints' scope (rationale only) but named by no Plan task, so recorded here rather than ticked.
Checks run: `git diff --stat` (NOTES.md and this log only); Commands block unset, markdown-only repo, no test applies to non-normative rationale.
Left: nothing for agents; the remaining Done-when boxes and closing the spec are the human's.
PROPOSAL (if any): none.
