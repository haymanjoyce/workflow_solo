# Rules — spec-driven solo workflow
Version: 1.0 · Status: approved

These rules and AGENTS.md bind every agent here; agents follow AGENTS.md
as written, and neither file restates the other. No vendor tool, memory
feature or chat product is part of the system.
- Continuity lives in git, never in a chat thread or vendor memory.
- No code until the human approves the spec by setting Status: approved.
- Agents communicate only through the repo; handoff is git, not a paste.
- One active feature spec at a time. Maintenance has its own lane.

## Layout (day zero)
README.md, RULES.md, NOTES.md, AGENTS.md; docs/: product.md,
commissioning.md, assurance-log.md; specs/: TEMPLATE.md, TEMPLATE-hotfix.md,
_active.md, done/; src/ and tests/, empty until the first approved task.
No plugins, second chat product or vendor rule files at day zero.

## Authority
A spec's contract is its Goal, Done when, Non-goals and Constraints.

| Artefact | Role | Changed by |
|---|---|---|
| docs/product.md | what, for whom, constraints, non-goals | human, rarely |
| specs/<name>.md | one unit of work | per the spec rows below |
| Spec contract | frozen once approved | human, always |
| Spec Status | lifecycle: draft, approved, done | human |
| Spec Plan | working notes: the task list | human; agent per AGENTS.md |
| Plan task boxes | progress | human may tick; agent per AGENTS.md |
| Done-when boxes | acceptance | human only |
| Session log | working notes | agent appends; human may annotate |
| specs/_active.md | sole authority for what is in play | human |
| AGENTS.md | how any agent behaves here | human, rarely |
| README.md | human orientation | as needed |
| src/, tests/ | the product | human; agent within the spec's Constraints |

## Active spec and hotfix lane
specs/_active.md says what is in play; a spec's Status says where it is
in its lifecycle. If they disagree, the agent stops and asks, and the
human fixes _active.md. It has two lines, `active: specs/<name>.md` and
`hotfix: specs/hotfix-<name>.md`, each `none` when nothing is in play.
A hotfix spec may coexist with the active feature spec; at most one
hotfix is in play. It restores existing behaviour to its working or
documented state, with no new capability, interface change or scope;
new behaviour needs a queued feature spec (agent side: AGENTS.md).

## Git, review and size
- The human's spec and doc edits are their own commits.
- Main-only is fine until a hotfix must land mid-feature. Then the
  feature task in progress moves to a branch, the hotfix lands on main
  and the branch rebases. Feature and hotfix never share a session.
- The human reviews the diff plus the log's claims, not a chat transcript.
- Split a spec when its Plan passes about a day of tasks, or its Session
  log a week of entries.

## Closing a spec
The human ticks every Done-when box against observed behaviour, sets
Status: done, moves the file to specs/done/ (hotfixes too) and sets
_active.md to none or the queued next spec. Durable commands and
conventions go to AGENTS.md, product truths to docs/product.md. Nothing
durable stays only in a done spec; finished work never stays active.

## Commissioning, drills and templates
Commissioning is required before the real product starts, and the fire
drill recurs after it: both are the human's procedures, held in
docs/commissioning.md. Feature specs follow specs/TEMPLATE.md; hotfix
specs follow specs/TEMPLATE-hotfix.md.
