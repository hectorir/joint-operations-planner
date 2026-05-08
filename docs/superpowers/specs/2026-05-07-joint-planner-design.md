# Joint Planner — Design Spec

**Date:** 2026-05-07
**Status:** Approved
**Plugin:** `joint-planner` v0.1.0
**Repo:** https://github.com/hectorir/joint-operations-planner

---

## 1. Purpose

A doctrinal joint planning copilot for Claude Code. Walks military planners through the seven-step Joint Planning Process (JPP) defined in JP 5-0 (1 December 2020), produces planning artifacts grounded in doctrine, and red-teams existing drafts against the publication's checklists.

The plugin's distinguishing claim is *fidelity to JP 5-0*. Every skill embeds or references the relevant section of a Practitioner Field Guide that condenses the publication, and every plan artifact is validated against an explicit rubric drawn from the field guide.

## 2. Non-goals (v1)

- TPFDD / TPFDL generation.
- CONPLAN / OPLAN annex generation (Levels 3 and 4).
- Live integration with GFM, JOPES, JS J-5, or any DoD information system.
- Classification handling. The plugin is **UNCLASSIFIED-only**. Classified information must not be entered.
- Multi-user / collaborative plan editing.
- Retrieval over the source JP 5-0 PDF. The Practitioner Field Guide is the authoritative source for v1.
- A web UI. (Phase 2 deliverable, designed to wrap the same plan-dir model.)

## 3. Architecture

Four layers:

1. **Invocation surface** — slash commands and the `joint-planner` agent (`subagent_type` for the Agent tool).
2. **Skills layer** — one skill per command. Each skill is stateless: read manifest + relevant files + doctrine, work with the planner, write back. Skills do not call each other directly.
3. **Knowledge layer** — static, shipped with the plugin: `references/jp5-0-field-guide.md`, `references/templates/`, `references/checklists/`, `references/rubrics/`.
4. **Plan workspace** — per-plan directory on the planner's local disk: `~/joint-plans/<plan>/`, with a `manifest.yaml`, a `context.md`, numbered step folders, and a git history.

### 3.1 Invocation surface

```
/jp                       Top-level router (front door).
/jp-status [plan]         Where am I? Step status, gaps, recommended next.

# Per-mode (the planner knows what kind of help they want)
/jp-plan                  Sherpa — walk me through a step.
/jp-coach                 Doctrinal explanation, quizzing.
/jp-critique              Red-team a draft against the rubric.
/jp-generate              Produce an artifact (brief, CONOPS, OPORD shell, etc.).

# Per-step (planner knows which step they're in; mode inferred from state)
/jp-initiation            Step 1.
/jp-mission-analysis      Step 2 (the heaviest skill).
/jp-coa-development       Step 3.
/jp-wargame               Step 4 — COA Analysis & Wargaming.
/jp-coa-comparison        Step 5.
/jp-coa-approval          Step 6.
/jp-plan-development      Step 7.

# Special-purpose helpers
/jp-cog                   COG / critical-factors analysis (cross-cuts steps).
/jp-risk                  Risk assessment (P × C, mitigation, civilian script).
/jp-assess                Operation assessment plan (MOEs, MOPs, indicators).
```

### 3.2 Mode inference

Within a per-step skill, mode is inferred from state and intent:

- Empty step folder → **sherpa**.
- Existing draft + planner brings new info → **sherpa** (revise).
- Existing draft + planner says "review" or invokes `/jp-critique` → **critic**.
- Planner says "give me the brief" or invokes `/jp-generate` → **generator**.
- `/jp-coach` invocation → **coach** (does not write to plan dir).

## 4. Plan-directory layout

```
~/joint-plans/<plan-name>/
├── README.md                      # human-friendly overview
├── manifest.yaml                  # plan level, step status, links (single source of truth)
├── context.md                     # plan-specific situational frame
│
├── 00_initiation/
│   ├── strategic_guidance.md
│   ├── initial_planning_guidance.md
│   └── operational_approach.md
│
├── 01_mission_analysis/
│   ├── facts.md
│   ├── assumptions.md
│   ├── constraints_restraints.md
│   ├── tasks.md                   # specified | implied | essential
│   ├── mission_statement.md
│   ├── ccirs.md
│   ├── cogs.md                    # links to /cog/
│   ├── risk_assessment_initial.md
│   ├── coa_evaluation_criteria.md
│   └── operational_approach.md    # refined; supersedes 00_initiation copy
│
├── cog/                           # cross-cutting
│   ├── friendly.md
│   └── threat.md
│
├── 02_coas/
│   └── coa-NN-<short-name>.md     # one file per COA, validity tests inline
│
├── 03_wargame/
│   ├── most-likely-enemy-coa.md
│   ├── most-dangerous-enemy-coa.md
│   ├── coa-NN-vs-likely.md        # action → reaction → counteraction log
│   ├── coa-NN-vs-dangerous.md
│   ├── synchronization_matrix.md
│   └── decision_support.md        # DST, decision points, branches/sequels
│
├── 04_comparison/
│   └── comparison_matrix.md
│
├── 05_approval/
│   └── decision.md                # selected COA + acceptable risk statement
│
├── 06_plan/
│   ├── concept_of_operations.md
│   ├── major_forces.md            # BPLAN only
│   ├── support_concept.md         # BPLAN only
│   ├── timeline.md                # BPLAN only
│   └── shortfalls.md
│
├── assess/                        # cross-cutting
│   ├── moes.md
│   ├── mops.md
│   └── indicators.md
│
└── log/
    ├── decisions.md
    ├── changes.md
    ├── critiques/                 # one file per critic-mode invocation
    └── transcripts/               # optional saved sessions
```

### 4.1 manifest.yaml schema

Schema documented in detail in `references/templates/manifest.yaml`. Key fields:

- `plan.name`, `plan.level` (`estimate` or `bplan`), `plan.dir`.
- `steps.<step>.status` (`pending` / `in_progress` / `complete` / `stale`), `last_modified`, `last_critique`.
- `cross_cutting.cog`, `cross_cutting.assess` — tracked separately.
- `coas[]` — each with `id`, `short_name`, `file`, `validity` (5 tests), `wargamed.most_likely`, `wargamed.most_dangerous`, `selected`.
- `approved_coa` — filled at Step 6.
- `iteration.wargame_rounds`, `iteration.reentries[]` — log of `{step, timestamp, reason}`.
- `stale[]` — auto-populated artifacts when re-entering an upstream step.

### 4.2 Plan-dir contracts (skill invariants)

1. Manifest exists. Skills error if missing; never silently work without state.
2. Step folders pre-exist at init (predictable globs).
3. Filenames are conventional: `coa-NN-<kebab>.md`, `coa-NN-vs-{likely|dangerous}.md`, `<step>-<YYYY-MM-DD-HHMM>.md` for critiques.
4. `context.md` exists at plan root, possibly empty.
5. Git is initialized at plan creation; auto-commit on step transitions with structured messages.
6. No skill mutates files outside its step folder, the manifest, and `log/`.

### 4.3 Skill coordination

Skills coordinate through the plan dir, not direct calls. Three mechanisms:

1. **Linearity gate.** A per-step skill refuses to start if upstream steps are `pending`, with `--force` override.
2. **Stale propagation.** Re-entering an earlier step marks downstream `complete` steps as `stale`. `/jp-status` surfaces this.
3. **Auto-critique gate.** A skill cannot transition `in_progress` → `complete` without `/jp-critique` (in dry-run) returning zero `FAIL`s. `WARN`s do not block.

Single-writer per session; no concurrent-edit conflict resolution in v1.

## 5. Doctrinal grounding

Field guide is the canonical source. Every skill that performs doctrinal work either:

- embeds verbatim the relevant field-guide section in its prompt (for short sections), or
- directs the agent to `Read references/jp5-0-field-guide.md` and load specific sections by anchor.

The full field guide ships at `references/jp5-0-field-guide.md`. Templates ship at `references/templates/`. Checklists at `references/checklists/`. Rubrics at `references/rubrics/`.

Field-guide sections embedded per skill:

| Skill | Embedded sections |
|---|---|
| `/jp` | §1 Quick Reference, §2.5 seven principles, §5.1 JPP map |
| `/jp-status` | §11.4 MOPs/MOEs hierarchy, §11.5 four outcomes, §13 |
| `/jp-initiation` | §5.2, §6.1 op design 9-step, §6.2 OE frameworks, §6.3 problem definition, §6.4 operational approach |
| `/jp-mission-analysis` | §5.3 entire, §2.4 problem understanding, §13.1, §13.2 |
| `/jp-coa-development` | §5.4 (5 validity tests), §7.2, §7.5–7.7, §7.9, §13.3 |
| `/jp-wargame` | §5.5, §7.10, §13.4 |
| `/jp-coa-comparison` | §5.6 |
| `/jp-coa-approval` | §5.7, §10.4 |
| `/jp-plan-development` | §5.8, §4 orders, §13.5 |
| `/jp-plan` | §1, §2.5, sherpa role guidance |
| `/jp-coach` | §14 glossary + index of all sections |
| `/jp-critique` | §13.2/3/4/5, §8.6 COG completion 5Qs, §10.4, all rubrics |
| `/jp-generate` | §4 orders cheat-sheet, §4.3 5-para format, all relevant templates |
| `/jp-cog` | §8 entire |
| `/jp-risk` | §5.3.6, §10, §13.6 |
| `/jp-assess` | §11 entire |

## 6. The two trickiest skills

### 6.1 `/jp-wargame` — interactive multi-cell roleplay

The planner is **Blue**. The agent plays **Red** aggressively (J-2-led, with realistic capabilities). The agent narrates **Green** (transnational/NGO/other actors) when relevant, and adjudicates as **White** at the end of each cycle.

Round structure (per critical event, per COA, against most-likely AND most-dangerous enemy COA):

1. White (agent): state critical event and starting conditions.
2. Blue (planner): friendly action.
3. Red (agent): enemy reaction — full realistic capability set.
4. Blue (planner): friendly counteraction.
5. White (agent): adjudicate; log to sync matrix; flag refined CCIRs, branches, sequels, shortfalls.
6. White (agent): "stop and revise, or push to next event?"

Discipline guards (enforced by the skill's prompt):

- Refuses to patch the COA mid-wargame. Stop, revise, restart.
- Self-corrects soft Red-cell play.
- Refuses completion of the wargame artifact until both most-likely and most-dangerous enemy COAs have been run against every retained friendly COA.

Outputs: `03_wargame/most-likely-enemy-coa.md`, `most-dangerous-enemy-coa.md`, per-pair logs, `synchronization_matrix.md`, `decision_support.md`.

### 6.2 `/jp-critique` — structured red-team findings

For each rubric line item: render `PASS` / `WARN` / `FAIL` + quote + doctrinal cite + remediation.

Findings written to `log/critiques/<step>-<YYYY-MM-DD-HHMM>.md`. The draft itself is **never mutated** — the planner is the author; the critique is peer review they choose to act on.

For final-plan check (`/jp-critique --step plan`) the skill also runs the §13.5 two-line test:

1. Achieves the objective at acceptable risk.
2. Does not foreclose future options.

Self-critique: every per-step skill calls `/jp-critique` in dry-run mode before transitioning a step to `complete`. Any `FAIL` keeps the step `in_progress`.

## 7. Distribution

- Source repo: `~/code/joint-planner/` (this directory) → https://github.com/hectorir/joint-operations-planner.
- Install during development: load the local plugin via Claude Code's plugin loader.
- Future: publish to a personal marketplace (out of scope for v1).

## 8. Worked example

`examples/exercise-pacific-cyclone/` — a fictional UNCLASSIFIED HADR scenario (cyclone strikes the fictional Republic of Cernavia; CCMD directed to plan a JTF response in support of USAID). Plan level: BPLAN. All seven steps complete. Demonstrates the file structure, manifest state, and artifact format end-to-end.

The scenario is deliberately fictional to avoid geopolitical sensitivity while exercising interagency coordination, multinational coordination, stabilization mechanisms, and a credible threat actor (criminal networks exploiting chaos).

## 9. Testing

Three layers, all under `tests/`:

1. **Rubric tests** — for each rubric, a deliberately bad fixture seeds a violation; assert that `/jp-critique` catches the expected `FAIL`.
2. **State-machine tests** — script the plan-dir lifecycle (create → mission analysis → wargame → re-enter Step 3 → confirm wargame stale).
3. **End-to-end smoke** — copy worked example fresh, run `/jp-status`, verify reported state matches.

Tests are invoked via `tests/run.sh` using headless `claude` invocations.

## 10. Personalization

- **Profile** (`~/.config/joint-planner/profile.md`): planner-level defaults — preferences, recurring strategic guidance citations, default plan level. Optional. Empty profile = generic experience.
- **Per-plan context** (`<plan>/context.md`): plan-specific situational frame — higher HQ, OE, stakeholders, strategic guidance citations *for this plan*.
- Plan-level overrides profile on conflict.

Skills read both, asking the planner to populate fields they need if missing.

## 11. UNCLASSIFIED guardrail

The umbrella agent's prompt and the README state:

> This plugin is for UNCLASSIFIED training and unclassified planning support only. The plugin runs through Anthropic's API and reads/writes files on the planner's local disk. Classified information must not be entered.

This is a non-negotiable constraint of v1.
