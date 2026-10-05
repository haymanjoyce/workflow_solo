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
- [x] task 1 — inventory: map every normative rule and every rationale
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

### 2026-10-05 — session 3 (task 1)
Agent/tool: Claude Code (Opus 5.5)
Did: task 1, the inventory. Every normative rule (R) and rationale
passage (W) in WORKFLOW.md §1–§13 is mapped to its destination below.
"L" cites v1 WORKFLOW.md lines at commit 8539f2d. Destinations that
already exist cite their line: AGENTS.md:N, TEMPLATE.md:N
(specs/TEMPLATE.md), HOTFIX.md:N (specs/TEMPLATE-hotfix.md). RULES.md,
NOTES.md and docs/commissioning.md don't exist yet, so they are cited
by planned section; task 2 swaps in line numbers. Every row has a
destination. No file other than this spec changed.

Map:

Header (L1–9)
- R L3–4 version 1.0, status approved → RULES.md header, version
  unchanged (v2-commissioning owns the number)
- R L8–9 LM-agnostic: no vendor tool, memory feature or chat product
  is part of the system → RULES.md Principles; the memory clause is
  AGENTS.md:13–14
- W L5–8 purpose of the document → NOTES.md

§1 Principles
- R L15–17 continuity lives in git, never in a chat or vendor memory →
  RULES.md Principles (git half); AGENTS.md:13–14 (memory half)
- W L15–16 "agents are stateless workers…" → NOTES.md
- R L18–19 no code until a spec is approved; approval is a human act
  recorded in files → AGENTS.md:21 (agent side); RULES.md Principles
  (approval = human sets Status: approved)
- R L20–21 agents communicate only through the repo; no paste between
  chats → RULES.md Principles
- R L22–23 one active feature spec at a time; maintenance has its own
  lane → RULES.md Principles, pointing to RULES.md Hotfix lane
- W L22 "two active specs is how agents invent scope" → NOTES.md
- R L24–26 contract and scratch are separate; changing the contract is
  always a human decision → RULES.md Authority; AGENTS.md:30;
  TEMPLATE.md:8,12,15 (CONTRACT markers)
- R L27–28 the workflow proves itself at commissioning and then
  periodically → RULES.md Commissioning (pointer only)

§2 Repo layout
- R L34–47 day-zero skeleton → RULES.md Layout, as a compact list. It
  adds RULES.md, NOTES.md and docs/commissioning.md (this spec's
  Goal), and docs/assurance-log.md, which §10/§13 require but §2
  omits (see question 3)
- R L45 src/ empty until the first approved task → RULES.md Layout
- W L46 "§5 requires a test per task" → no new home needed: it is a
  cross-reference, and the rule it cites is AGENTS.md:43–44
- R L49 no plugins, no second chat product, no vendor rule files at
  day zero → RULES.md Layout
- R L50–52 a tool's own entry file holds one line referring to
  AGENTS.md → AGENTS.md:5–6
- W L51–53 CLAUDE.md / .cursor/rules examples; "Adapters, not
  workflow" → NOTES.md (README.md also keeps the example)

§3 File contracts
- R L59–66 table: role and who changes each file → RULES.md Authority,
  merged with §4's matrix into one table to save lines. Human-only
  edits: AGENTS.md:29,31,32 (agent side)
- R L62 a spec's contract is frozen after approval → RULES.md Authority
- R L63 _active.md is the sole authority for what is in play →
  RULES.md Active spec
- R L64 hotfix specs: restore-only, changed as feature specs are →
  RULES.md Hotfix lane
- R L68–73 _active.md says what is in play, Status says lifecycle
  (draft|approved|done); if they disagree the agent stops and asks
  and the human fixes _active.md → RULES.md Active spec. General
  stop-and-ask: AGENTS.md:12
- W L71 "they are not duplicates" → NOTES.md

§4 Edit-authority matrix
- R L83–91 agent read-only rows (product.md, contract fields, Status,
  _active.md, AGENTS.md) → AGENTS.md:28–32; human "edit" column →
  RULES.md Authority
- R L86 Plan: human edits, agent proposes via the log → AGENTS.md:35–38;
  TEMPLATE.md:18
- R L87 Plan boxes: human may tick; agent only per the completion rule
  → RULES.md Authority (human side); AGENTS.md:40–48 (agent side)
- R L88 Done-when boxes: human only → AGENTS.md:33; TEMPLATE.md:8;
  HOTFIX.md:12
- R L89 Session log: human may annotate, agent appends → RULES.md
  Authority; TEMPLATE.md:22
- R L92 src/ and tests: agent edits within the approved spec's
  Constraints → RULES.md Authority
- W L79 "the governance core" and L94–102, why the two lines are hard
  → NOTES.md

§5 Task-completion rule
- R L108–120 the three conditions → AGENTS.md:40–47 (already holds
  them in full)
- W L118–120 why the agent/tool line exists (attribution; the drill
  depends on it) → NOTES.md
- R L122–123 the human reviews the diff plus the log's claims, not a
  transcript → RULES.md Review
- W L123–125 "diffs look plausible…" → NOTES.md

§6 Maintenance lane
- W L131–132 why a release valve → NOTES.md
- R L136–137 a hotfix may coexist with the feature spec; at most one
  hotfix in play → RULES.md Hotfix lane
- R L138–141 restore-only; no new capability, interface change or
  scope; new behaviour means a queued feature spec → AGENTS.md:24–26
  (agent side); HOTFIX.md:8–10; RULES.md Hotfix lane names the three
  forbidden changes and refers to AGENTS.md for the stop
- R L142–143 hotfixes need Status: approved before code → AGENTS.md:21
  (covers every spec)
- W L143–144 "template deliberately short" → NOTES.md
- R L145–147 separate sessions and commits; branch if feature work is
  mid-task → RULES.md Git (with §11's branching rule); commit half is
  AGENTS.md:52–53
- R L148 closed hotfixes move to specs/done/ → RULES.md Closing
- R L150–155 _active.md's two-line format → RULES.md Active spec, two
  lines, unfenced

§7 AGENTS.md copy
- R L159 "copy verbatim into the repo" → RULES.md Pointers: AGENTS.md
  is the sole copy and is followed as written. The verbatim-copy
  requirement is the duplication this spec's Goal retires; AGENTS.md
  keeps its force by being the only copy
- R L161–232 the fenced copy: each section now lives only in AGENTS.md
  (Role 3–6, Source of truth 8–14, Workflow 16–26, Never edit 28–33,
  Plan changes 35–38, Completing 40–48, Git 50–55, Commands 57–66,
  Conventions 68–70). Byte-identical to AGENTS.md today (diffed), so
  deleting it loses nothing

§8 Templates
- R L238–270 feature template → TEMPLATE.md:1–26, byte-identical
  (diffed); RULES.md Pointers names the file
- R L277–299 hotfix template → HOTFIX.md:1–18, byte-identical
  (diffed); RULES.md Pointers names the file
- R L272–273 sizing: a Plan over roughly a day of tasks means split
  the spec → RULES.md Spec size
- R L273–275 bloat signal: a log past a week of entries means split →
  RULES.md Spec size; W "long-thread rot" → NOTES.md

§9 Commissioning
- R L305–306 no real product until one fake feature has been through
  the loop → RULES.md Commissioning ("required before real work; see
  docs/commissioning.md", tests not described); procedure in
  docs/commissioning.md
- R L308–360 dummy, notes placement, steps 1–11, two-agent bar →
  docs/commissioning.md, verbatim apart from repointed cross-references
  (question 4)
- W L310–319 why notes live outside the repo (blind results) →
  docs/commissioning.md, not NOTES.md (question 1)

§10 Fire drill
- W L366–367 instruction-following degrades → NOTES.md
- R L369–376 when to re-run A–D, what D needs, log format, two
  consecutive failures → docs/commissioning.md; RULES.md Commissioning
  says drills are required and names the file. The log format also
  sits in docs/assurance-log.md's table header

§11 Git discipline
- R L382–383 one commit per task, message format → AGENTS.md:51
- R L383–384 the human's spec/doc edits are their own commits →
  RULES.md Git
- R L385 the agent commits its completed task at session end →
  AGENTS.md:48
- R L386 the human alone pushes, merges and tags → AGENTS.md:54
- R L387–390 main-only until a hotfix lands mid-feature, then branch,
  hotfix on main, branch rebases; never interleave in one commit or
  session → RULES.md Git (session half); AGENTS.md:52–53 (commit half)
- W L391–393 why granularity is a rule (one-commit revert) → NOTES.md

§12 Closing a spec
- R L399–400 the human ticks every Done-when box against behaviour →
  RULES.md Closing; AGENTS.md:33 (agent side)
- R L401–402 Status: done, move to specs/done/, _active.md to none or
  the next spec → RULES.md Closing
- R L403–405 promote durable commands and conventions to AGENTS.md,
  product truths to product.md; nothing durable only in a done spec →
  RULES.md Closing
- R L406–407 never leave finished work in the active slot → RULES.md
  Closing; W "open invitation…" → NOTES.md

§13 Build checklist
- R L413–430 → docs/commissioning.md, since it closes on commissioning
  and refusal tests. Two items reword because their targets move:
  L418 "AGENTS.md matches §7 verbatim" becomes "AGENTS.md present"
  (the retired verbatim rule), and L419 "both templates of §8"
  becomes the two file names (question 2)

RULES.md budget check (planned sections, approximate lines): header 4,
Principles 7, Layout 7, Authority table 14, Active spec 5, Hotfix lane
5, Review 2, Git 4, Spec size 2, Closing 6, Commissioning 2, Pointers
3 = 61, with 5 lines to spare against the 66-line cap.

Checks run: none — AGENTS.md's Commands block has no values in this
markdown-only repo, so there is nothing to run. diff confirmed
WORKFLOW.md L162–231 = AGENTS.md, L241–269 = specs/TEMPLATE.md and
L280–298 = specs/TEMPLATE-hotfix.md. No test written: docs-only
inventory with no executable behaviour.
Left: tasks 2 and 3. The human reviews this map before task 2.
PROPOSAL (if any): none to the Plan. Questions for the map review:
1. §9's blind-test reasoning (L310–319) stays with the procedure in
   docs/commissioning.md, so NOTES.md describes no refusal test.
   Agree, or move it to NOTES.md?
2. §13 goes to docs/commissioning.md, with L418 and L419 reworded as
   above. Agree, or should the build checklist sit in RULES.md minus
   its commissioning item?
3. RULES.md Layout lists docs/assurance-log.md, which v1 §2 omits but
   §10/§13 require. Is that a fix in scope, or a meaning change to
   leave out?
4. Moved text cites "§5", "§10" and so on. Task 2 would repoint these
   to file and section names (e.g. "AGENTS.md, Completing a task").
   Any objection?
5. §1.5 (L24–25) names three contract fields; §4 and AGENTS.md:30 name
   four, adding Constraints. RULES.md would use the four. No force is
   lost, but please confirm.
