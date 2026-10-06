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
- [x] task 2 — per the approved map: write RULES.md (≤66 lines; §7 and
      §8 become pointers to AGENTS.md and the template files), NOTES.md
      and docs/commissioning.md, and delete WORKFLOW.md, all in one
      commit, so no rule is ever homeless
- [x] task 3 — repoint citations: README.md, docs/assurance-log.md's
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

### 2026-10-05 — session 3 (map review)
Agent/tool: Claude Code (Opus 5.5)
Did: recorded the human's review of session 3's map. The human
approved the map as written and answered yes to all five questions,
taking each recommendation:
1. §9's blind-test reasoning goes to docs/commissioning.md; NOTES.md
   describes no refusal test.
2. §13 goes to docs/commissioning.md; L418 becomes "AGENTS.md present"
   and L419 names specs/TEMPLATE.md and specs/TEMPLATE-hotfix.md.
3. RULES.md Layout lists docs/assurance-log.md.
4. Task 2 repoints "§N" citations in moved text to file and section
   names.
5. RULES.md names four contract fields, Constraints included.
Task 2 implements the map with these answers. No other file changed.
Checks run: none — log-only change; Commands block has no values.
Left: tasks 2 and 3, each in its own session.
PROPOSAL (if any): none.

### 2026-10-05 — session 4 (task 2)
Agent/tool: Claude Code (Opus 5.5)
Did: task 2, per session 3's map and the human's review. Wrote RULES.md
(66 lines), NOTES.md and docs/commissioning.md, and deleted WORKFLOW.md
(`git rm`), in one commit. Layout changes from the planned sections, to
fit 66 lines: Principles sit under the opening paragraph with no
heading; "Pointers" folded into that paragraph (AGENTS.md) and the
last section (templates); Review, Git and Spec size share one section;
the Active spec and Hotfix lane sections are merged. _active.md's
format is written inline, not as a two-line block.
Line resolution of session 3's map. Each row's planned destination
section resolves to these lines; AGENTS.md, TEMPLATE.md and HOTFIX.md
citations are unchanged, since none of those files changed.
- Header: L3–4 → RULES.md:2; L8–9 → RULES.md:5–6; W L5–8 → NOTES.md:7–10
- §1: L15–17 → RULES.md:7; W L15–16 → NOTES.md:12–15; L18–19 →
  RULES.md:8; L20–21 → RULES.md:9; L22–23 → RULES.md:10, with the lane
  at RULES.md:41–44; W L22 → NOTES.md:17–18; L24–26 → RULES.md:19,25;
  L27–28 → RULES.md:63–65
- §2: L34–47 → RULES.md:13–15; L45 → RULES.md:15; L49 → RULES.md:16;
  W L51–53 → NOTES.md:47–50
- §3: L59–66 → RULES.md:21–34; L62 → RULES.md:25; L63 → RULES.md:31;
  L64 → RULES.md:24,41–44; L68–73 → RULES.md:37–39; W L71 →
  NOTES.md:24–28
- §4: L83–91 human column → RULES.md:23–33; L86 → RULES.md:27; L87 →
  RULES.md:28; L89 → RULES.md:30; L92 → RULES.md:34; W L79, L94–102 →
  NOTES.md:30–39
- §5: W L118–120 → NOTES.md:44–45; L122–123 → RULES.md:51; W L123–125
  → NOTES.md:41–43
- §6: W L131–132 → NOTES.md:19–21; L136–137 → RULES.md:41–42; L138–141
  → RULES.md:42–44; W L143–144 → NOTES.md:21–22; L145–147 →
  RULES.md:48–50; L148 → RULES.md:57; L150–155 → RULES.md:39–40
- §7: L159 → RULES.md:4–5 (AGENTS.md followed as written; it is the
  sole copy); L161–232 → AGENTS.md as mapped
- §8: L238–270 → RULES.md:65 names specs/TEMPLATE.md; L277–299 →
  RULES.md:65–66 names specs/TEMPLATE-hotfix.md; L272–275 →
  RULES.md:52–53; W "long-thread rot" → NOTES.md:52–55
- §9: L305–306 → RULES.md:63 and docs/commissioning.md:8–9; L308–360
  → docs/commissioning.md:11 (dummy), 13–22 (notes placement, with the
  blind-test reasoning), 24–59 (steps 1–11), 61–64 (two-agent bar)
- §10: W L366–367 → NOTES.md:65–67; L369–376 → docs/commissioning.md:
  68–75 and RULES.md:63–65
- §11: L383–384 → RULES.md:47; L387–390 → RULES.md:48–50; W L391–393 →
  NOTES.md:57–59
- §12: L399–400 → RULES.md:56; L401–402 → RULES.md:56–58; L403–405 →
  RULES.md:58–60; L406–407 → RULES.md:60; W → NOTES.md:61–63
- §13: L413–430 → docs/commissioning.md:77–95; L418 at :83, L419 at :84
Moved text in docs/commissioning.md repoints its citations: §5 →
AGENTS.md's "Completing a task", §10 → "Fire drill, below", §9 →
"Commissioning, above", §2 → RULES.md's Layout. Otherwise §9, §10 and
§13 are v1's text.
Checks run: AGENTS.md's Commands block has no values (markdown-only
repo), so there is no test or lint to run. Shell: Git Bash. Ran the
Done-when checks that apply to this task:
`wc -l RULES.md` → 66; `awk 'length>80' RULES.md` → nothing;
`grep -inE 'rationale|because' RULES.md` → nothing;
`grep -rl "## Role of this file" .` → ./AGENTS.md alone;
`git ls-files` shows no WORKFLOW.md and does show RULES.md, NOTES.md
and docs/commissioning.md once committed. No test written: docs-only
task with no executable behaviour.
Left: task 3. Until it lands, README.md and docs/assurance-log.md
still cite WORKFLOW.md, which no longer exists. Task 3's AGENTS.md edit
may shift AGENTS.md's line numbers, which the map cites.
PROPOSAL (if any): `.gitignore` line 2 also cites "WORKFLOW.md §9".
It is not in this spec's Files in scope, but the Done-when's
`grep -rn WORKFLOW.md` will find it. Suggest the human adds
`.gitignore` to task 3 (repoint to docs/commissioning.md), or edits it
directly. Separately, that grep will also hit this spec and the other
v2 specs until they move to specs/done/.

### 2026-10-05 — session 5 (task 3)
Agent/tool: Claude Code (Opus 5.5)
Did: task 3. The human had already made the AGENTS.md reading-list
change and repointed `.gitignore` themselves (commit 7704c59), so this
session did not edit AGENTS.md and needed no scribe authorisation.
Repointed the rest:
- README.md: the file list names RULES.md (read first), NOTES.md
  (non-normative) and docs/commissioning.md (the human's procedures,
  not for agents) in place of WORKFLOW.md. "Starting a new project"
  step 2 names docs/commissioning.md. "Pointing an agent" now reads
  "Follow RULES.md; AGENTS.md governs your behaviour." and names
  neither NOTES.md nor docs/commissioning.md. The adapter rule cites
  AGENTS.md's "Role of this file" instead of §2. "Keeping it honest"
  cites docs/commissioning.md's Fire drill section instead of §9/§10.
  "Iterating the workflow" names RULES.md/AGENTS.md.
- docs/assurance-log.md heading: "(docs/commissioning.md, Fire drill)"
  instead of "(WORKFLOW.md §10)".
Checks run: AGENTS.md's Commands block has no values (markdown-only
repo), so there is no test or lint to run. Shell: Git Bash. Done-when
greps:
`grep -rln WORKFLOW.md --exclude-dir=.git .` → specs/done/
template-hardening.md and this spec only;
`grep -rl "## Role of this file" --exclude-dir=.git .` → AGENTS.md and
this spec (its own Done-when quotes the string);
`grep -nE "NOTES.md|commissioning.md" AGENTS.md CLAUDE.md` and the same
over README's "Pointing an agent" section → nothing;
`git ls-files | grep -v '^specs/done/' | xargs grep -niE
"verbatim|byte-for-byte|byte-identical"` → this spec only, which
describes the retired rule and requires nothing.
No test written: docs-only task with no executable behaviour.
Left: all Plan tasks are done; the Done-when boxes are the human's.
Two things the human may want to know when ticking them:
1. Two Done-when greps match this spec's own text (WORKFLOW.md; "##
   Role of this file"). The first clears when the spec moves to
   specs/done/; the second still matches there, because `grep -rl`
   has no specs/done/ exclusion in that line.
2. AGENTS.md:17, the human's reading-list edit, is 88 characters. No
   rule caps AGENTS.md line length; mentioned only because RULES.md
   holds itself to 80. The edit also moved later AGENTS.md lines up by
   one, so session 3's map citations from AGENTS.md:18 onward are one
   line high.
PROPOSAL (if any): none.

### 2026-10-06 — session 6 (map citation correction)
Agent/tool: Claude Code (Opus 5.5)
Did: corrected line citations in session 3's map, found while the human
checked Done-when item 4. Every rule still lives where the map says;
only the line numbers below were wrong. Two causes:
1. Session 3's TEMPLATE.md and HOTFIX.md citations were one line short
   from the start. Neither file has changed since 13b344e.
2. The human's AGENTS.md reading-list edit (7704c59) joined two lines
   into one, so every AGENTS.md citation from line 18 onward is now one
   line high. Citations of AGENTS.md:5–6, :12 and :13–14 stand.
Corrections, by map row (old → current):
- §1 L18–19 draft gate: AGENTS.md:21 → :20
- §1 L24–26 contract: AGENTS.md:30 → :29; TEMPLATE.md:8,12,15 → :9,13,16
- §2 W L46 test rule: AGENTS.md:43–44 → :42–43
- §3 L59–66 human-only edits: AGENTS.md:29,31,32 → :28,30,31
- §4 L83–91 agent read-only rows: AGENTS.md:28–32 → :27–31
- §4 L86 Plan: AGENTS.md:35–38 → :34–37; TEMPLATE.md:18 → :19
- §4 L87 Plan boxes, agent side: AGENTS.md:40–48 → :39–47
- §4 L88 Done-when boxes: AGENTS.md:33 → :32; TEMPLATE.md:8 → :9;
  HOTFIX.md:12 → :13
- §4 L89 Session log: TEMPLATE.md:22 → :23
- §5 L108–120 the three conditions: AGENTS.md:40–47 → :39–46
- §6 L138–141 restore-only: AGENTS.md:24–26 → :23–25; HOTFIX.md:8–10 →
  :9–11
- §6 L142–143 hotfix approval: AGENTS.md:21 → :20
- §6 L145–147 commit half: AGENTS.md:52–53 → :51–52
- §7 L161–232 AGENTS.md sections: Workflow 16–26 → 16–25, Never edit
  28–33 → 27–32, Plan changes 35–38 → 34–37, Completing 40–48 → 39–47,
  Git 50–55 → 49–54, Commands 57–66 → 56–65, Conventions 68–70 →
  67–69. Role 3–6 and Source of truth 8–14 stand
- §8 L238–270 feature template: TEMPLATE.md:1–26 → :1–29
- §8 L277–299 hotfix template: HOTFIX.md:1–18 → :1–19
- §11 L382–383 commit message: AGENTS.md:51 → :50
- §11 L385 commit at session end: AGENTS.md:48 → :47
- §11 L386 push/merge/tag: AGENTS.md:54 → :53
- §11 L387–390 commit half: AGENTS.md:52–53 → :51–52
- §12 L399–400 agent side: AGENTS.md:33 → :32
Session 3's question 5 also cites AGENTS.md:30; that is now :29.
Session 4's RULES.md, NOTES.md and docs/commissioning.md citations were
checked line by line against the files and stand.
Checks run: Shell: Git Bash. `cat -n` of AGENTS.md, specs/TEMPLATE.md,
specs/TEMPLATE-hotfix.md, RULES.md and docs/commissioning.md, compared
with each cited line; `git show 8539f2d:AGENTS.md` to confirm the
pre-edit numbering; `git log -- specs/TEMPLATE.md
specs/TEMPLATE-hotfix.md` → 13b344e only. No test: log-only change.
Left: the human's Done-when review, from item 4 on.
PROPOSAL (if any): none.
