# Spec: v2-structure

Status: approved
Created: 2026-10-05

## Goal
An agent in a repo made from this template finds every rule it is bound
by in two short files, RULES.md and AGENTS.md, without wading through
rationale or the human's test procedures. A human who wants the reasons
reads NOTES.md. The human's commissioning and drill procedures live in
docs/commissioning.md, normative but on no agent's reading list.
WORKFLOW.md no longer exists. AGENTS.md and the two spec templates each
exist in exactly one copy, so changing one is a one-file edit with no
rule requiring a second, byte-identical copy to change with it.

## Done when            <!-- CONTRACT — human edits, human ticks -->
- [ ] WORKFLOW.md is absent from the tracked tree; RULES.md, NOTES.md
      and docs/commissioning.md are present (`git ls-files`)
- [ ] RULES.md is at most 66 lines (`wc -l`), none longer than 80
      characters
- [ ] RULES.md holds no rationale: `grep -inE 'rationale|because'
      RULES.md` returns nothing
- [ ] This spec's Session log holds a rule-by-rule mapping of v1
      WORKFLOW.md §1–§13, and every normative rule in it names a line
      in RULES.md, AGENTS.md, docs/commissioning.md or a template file
      where it now lives; no row reads "dropped"
- [ ] NOTES.md's first paragraph says it is non-normative and that
      RULES.md and docs/commissioning.md win wherever they disagree
      with it
- [ ] docs/commissioning.md holds v1 §9 and §10's procedures. RULES.md
      states that commissioning and drills are required and names
      docs/commissioning.md, without describing the refusal tests
- [ ] Only AGENTS.md contains AGENTS.md's text: `grep -rl "## Role of
      this file"` returns AGENTS.md alone, and RULES.md refers to
      AGENTS.md by name
- [ ] RULES.md, NOTES.md and docs/commissioning.md hold no fenced copy
      of either spec template; RULES.md names specs/TEMPLATE.md and
      specs/TEMPLATE-hotfix.md
- [ ] No tracked file outside specs/done/ requires AGENTS.md or a
      template to match another file verbatim or byte-for-byte
- [ ] AGENTS.md's every-session reading list names RULES.md; no agent
      reading list (AGENTS.md, CLAUDE.md, README's "Pointing an agent"
      instruction) names NOTES.md or docs/commissioning.md
- [ ] `grep -rn WORKFLOW.md` outside specs/done/ returns nothing

## Non-goals            <!-- CONTRACT -->
- Changing what any rule means. This spec moves and condenses text.
  The four rules the refusal tests probe (draft gate, "none" gate,
  contract-edit line, Plan-edit line) keep their exact force.
- A scribe role or a new Session log format (v2-scribe-and-logs).
- Any change to what commissioning, the fire drill or certification
  require, or to the template's version number (v2-commissioning).
  §9 and §10 move to docs/commissioning.md with their meaning
  unchanged.
- Subagent dispatch or a reviewer gate (v2-agents).
- Rewriting references to WORKFLOW.md inside specs/done/. Done specs
  are history.
- Application code. src/ stays empty.

## Constraints          <!-- CONTRACT -->
- Files in scope: WORKFLOW.md (deleted), RULES.md, NOTES.md and
  docs/commissioning.md (new), AGENTS.md (reading-list line only),
  README.md, docs/assurance-log.md (its heading cites WORKFLOW.md §10).
- AGENTS.md is human-edit-only under v1. Its one-line change needs the
  human's hand or a per-session scribe authorisation, recorded in the
  log, as template-hardening sessions 4 and 5 did.
- Each rule lives in one place. RULES.md and AGENTS.md must not restate
  each other's rules; one refers to the other.
- Markdown only. No dependencies, no tooling.
- Lands first of the four v2 specs. The others edit RULES.md, which
  this spec creates.

## Plan                 <!-- human edits; agents propose via log -->
- [ ] task 1 — inventory: map every normative rule and every rationale
      passage in WORKFLOW.md §1–§13 to its destination (RULES.md,
      AGENTS.md, docs/commissioning.md, a template file, or NOTES.md).
      Record the map in the Session log. No other file changes. The
      human reviews the map before task 2
- [ ] task 2 — per the approved map: write RULES.md (≤66 lines; §7 and
      §8 become pointers to AGENTS.md and the template files), NOTES.md
      and docs/commissioning.md, and delete WORKFLOW.md, all in one
      commit, so no rule is ever homeless
- [ ] task 3 — repoint citations: README.md, docs/assurance-log.md's
      heading, and AGENTS.md's reading list (scribe-authorised session)

## Session log          <!-- agents append; human may annotate -->
### 2026-10-05 — session 1 (drafting)
Agent/tool: Claude Code (Opus 5.5)
Did: drafted this spec from the human's brief, with Status: draft. No
other file changed by this spec.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): these are conflicts between the brief and v1's
rules, flagged here rather than resolved. Each needs the human's call
before approval.
1. RULES.md vs AGENTS.md. The brief makes RULES.md "what agents read",
   but under v1 agents read AGENTS.md. WORKFLOW.md is not on AGENTS.md's
   reading list; only README tells agents to follow it. Two normative
   files that agents read invite the drift that §7's byte-identical
   rule was built to stop. Done-when as drafted keeps both and has
   AGENTS.md name RULES.md, with a no-restating Constraint. The
   alternative is to fold AGENTS.md's rules into RULES.md and make
   AGENTS.md a one-line pointer. That would change §2, §3 and the
   adapter convention.
2. The page limit vs §9. I took "one page" to mean 66 lines, a printed
   page. §9's eleven-step commissioning procedure and §10's drill are
   normative but are the human's procedure, not the agent's. If they
   go into RULES.md, the agent's mandatory reading would describe the
   refusal tests and their wanted answers. §9's own blind-test
   reasoning argues against that, so they don't fit RULES.md on either
   count. Options: (a) a third, human-facing normative file (e.g.
   docs/commissioning.md) that no agent reading list names; (b) let
   v2-commissioning land first, so the procedure is already short.
   Note: v1 has a milder form of this already, since README tells
   agents to follow WORKFLOW.md, which contains §9.
3. §8's fenced templates duplicate specs/TEMPLATE.md and
   specs/TEMPLATE-hotfix.md, the same way §7 duplicates AGENTS.md. No
   rule keeps them in sync, so they can drift silently. The brief names
   only §7, so this spec does not touch §8. Suggest adding "§8 becomes
   pointers to the template files" to the Goal, or a Non-goal that
   explicitly keeps the duplicates.
4. Sequencing against run 2. Template-hardening session 10 and the
   standing sequence put the second-product commissioning pass next,
   against v1's rules. This spec changes no rule, but it does change
   which files run 2's sessions read, and it removes the verbatim check
   that run 1's conductor diffed. Decide whether run 2 goes before
   all four v2 specs or after them.
5. Drafting is itself unruled. AGENTS.md forbids an agent to edit "any
   spec's Goal, Done when, Non-goals, Constraints or Status". This
   session wrote all five, in a new file, at the human's request. I
   read that as creating, not editing, since nothing is contract until
   the human sets Status: approved. v1 does not say so. See
   v2-scribe-and-logs, whose scribe rule could cover it.

### 2026-10-05 — session 2 (drafting, decisions applied)
Agent/tool: Claude Code (Opus 5.5)
Did: wrote the human's answers to session 1's proposals into the
draft; Status stays draft. Decisions, in the human's chosen options:
1. "Both; no restating": no change; the draft already said so.
2. "Human-only normative file": §9 and §10 go to
   docs/commissioning.md, which no agent reading list names. Added to
   the Goal, Done-when, Constraints and Plan.
3. "Replace with pointers": §8's template copies go too. Added to the
   Goal, Done-when and task 2.
4. "After all four v2 specs": run 2 waits for the finished v2
   template and becomes its first certification. No change to this
   spec; recorded in v2-commissioning.
5. "Cover it in the Scribe rule": moved to v2-scribe-and-logs.
Checks run: none — markdown-only repo, Commands block unset.
Left: everything; the spec is unapproved.
PROPOSAL (if any): none open.
