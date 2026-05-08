# Joint Planner — A doctrinal joint planning copilot for Claude Code

> A Claude Code plugin that walks military planners through the seven-step Joint Planning Process (JPP) from **Joint Publication 5-0, *Joint Planning*** (Joint Chiefs of Staff, 1 December 2020). Provides structured plan workspaces, doctrinal critique, and artifact generation. UNCLASSIFIED only.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## What this is

`joint-planner` is a Claude Code plugin that turns a planning session with Claude into a doctrinally faithful walk through the Joint Planning Process. It supports four modes:

- **Sherpa** — walk me step-by-step through a JPP step.
- **Coach** — explain doctrine, quiz me, walk a worked example.
- **Critic** — red-team my draft against the doctrinal rubric.
- **Generator** — produce an artifact (mission analysis brief, CONOPS, OPORD shell, comparison matrix, etc.).

The plugin is grounded in a **Practitioner Field Guide to JP 5-0** that ships with the plugin (`references/jp5-0-field-guide.md`). Every skill embeds or references the relevant field-guide sections, and every plan artifact is validated against an explicit rubric drawn from the field guide.

## What it is **not**

- **Not a TPFDD/TPFDL generator.** Force-flow data is out of scope.
- **Not a CONPLAN/OPLAN annex generator.** v1 supports plan Levels 1 (Commander's Estimate) and 2 (BPLAN). Annexes A–Z are deferred.
- **Not classified-capable.** This plugin runs through Anthropic's API and reads/writes files on your local disk. **Do not enter classified information.**
- **Not a substitute for JP 5-0 itself.** For authoritative doctrine, ROE/RUF questions, multinational ratification details, and exact format guidance for orders, defer to the source publications listed at the bottom of the field guide.

## Hard rule

**UNCLASSIFIED only.** This plugin is for unclassified training and unclassified planning support. Classified information must not be entered. The umbrella agent will refuse to proceed if it detects classified content.

---

## Install

This plugin is not yet on a public marketplace. To install during development:

```bash
git clone https://github.com/hectorir/joint-operations-planner.git ~/code/joint-planner
# Then, in Claude Code:
/plugin install ~/code/joint-planner
/reload-plugins
```

## Quick start

```bash
# In Claude Code:
/jp                          # Front door — asks if you're starting fresh or continuing
```

The agent will:
1. Ask whether this is a new plan or an existing one.
2. If new: ask for a kebab-case name and plan level (`estimate` or `bplan`), then scaffold `~/joint-plans/<name>/` with all the JPP step folders, a `manifest.yaml`, and a `context.md`.
3. Run `git init` in the plan dir.
4. Dispatch to `/jp-initiation` to start Step 1.

## Slash commands

| Command | Purpose |
|---|---|
| `/jp` | Top-level router. Use when you don't know where to start. |
| `/jp-status [plan]` | Where am I? Reports step status, gaps, recommended next action. |
| `/jp-plan` | **Sherpa** — walk me through a step. |
| `/jp-coach` | **Coach** — explain doctrine, quiz me. |
| `/jp-critique [step]` | **Critic** — red-team a draft against the rubric. |
| `/jp-generate [artifact]` | **Generator** — produce a planning artifact. |
| `/jp-initiation` | JPP Step 1 — Planning Initiation. |
| `/jp-mission-analysis` | JPP Step 2 — Mission Analysis (the heaviest step). |
| `/jp-coa-development` | JPP Step 3 — COA Development. |
| `/jp-wargame` | JPP Step 4 — COA Analysis & Wargaming. |
| `/jp-coa-comparison` | JPP Step 5 — COA Comparison. |
| `/jp-coa-approval` | JPP Step 6 — COA Approval. |
| `/jp-plan-development` | JPP Step 7 — Plan or Order Development. |
| `/jp-cog [friendly\|threat]` | COG / critical-factors analysis. Cross-cuts steps. |
| `/jp-risk` | Risk assessment. P × C, mitigation, civilian-leader script. |
| `/jp-assess` | Operation assessment plan. MOEs / MOPs / indicators. |

## Plan workspace

Each plan lives in its own directory:

```
~/joint-plans/<plan-name>/
├── README.md
├── manifest.yaml                 # plan state — single source of truth
├── context.md                    # plan-specific situational frame
│
├── 00_initiation/
├── 01_mission_analysis/
├── cog/                          # cross-cutting
├── 02_coas/
├── 03_wargame/
├── 04_comparison/
├── 05_approval/
├── 06_plan/
├── assess/                       # cross-cutting
└── log/
    ├── decisions.md
    ├── changes.md
    └── critiques/                # one file per /jp-critique invocation
```

The plan dir is git-versioned automatically. Skills auto-commit at step transitions with structured messages (`step:mission-analysis complete`).

## Personalization

- **Profile** (optional): `~/.config/joint-planner/profile.md` — defaults that apply across all your plans (preferences, recurring strategic-guidance citations, default plan level).
- **Per-plan context** (always): `<plan>/context.md` — the situational frame for that plan (higher HQ, AOR, stakeholders, citations *for this plan*).

Per-plan context overrides profile defaults on conflict.

## Worked example

The plugin ships with a fully worked example: `examples/exercise-pacific-cyclone/`. It is a **fictional UNCLASSIFIED HADR scenario** (cyclone strikes the fictional Republic of Cernavia; CCMD directed to plan a JTF response in support of USAID). All seven JPP steps are scaffolded as `complete` and the artifacts demonstrate what each step's output looks like in finished form.

Use it to learn the workflow, browse what doctrinally-faithful artifacts look like, or copy fresh to `~/joint-plans/learn-jpp/` and walk yourself through.

## How it stays doctrinally faithful

1. **The Practitioner Field Guide is the canonical source.** It ships at `references/jp5-0-field-guide.md` and is the voice every skill quotes.
2. **Every skill embeds the relevant field-guide section** in its prompt (or directs the agent to `Read` it on entry).
3. **Critic mode walks an explicit rubric.** The rubrics in `references/rubrics/` enumerate the checks; critic mode renders PASS/WARN/FAIL with a quote, doctrinal cite, and remediation per item.
4. **Step transitions are gated.** A per-step skill cannot mark itself `complete` until critic-in-dry-run returns zero `FAIL`s.
5. **Stale propagation.** Re-entering an upstream step marks downstream artifacts `stale` automatically. JP 5-0 stop-revise-restart discipline is structurally enforced.

## Architecture

```
Invocation surface  (/jp slash commands · subagent_type:joint-planner)
        │
Skills layer  (one skill per command; share helpers; stateless)
        │
Knowledge layer  (jp5-0-field-guide.md · templates · checklists · rubrics)
        │
Plan workspace  (~/joint-plans/<plan>/ + manifest + git history)
```

See `docs/superpowers/specs/2026-05-07-joint-planner-design.md` for the full design.

## Roadmap (Phase 2)

- A local web UI that wraps the same plan-dir model. Forms per JPP step, rendered artifacts, search.
- Optional retrieval over the source JP 5-0 PDF for verbatim citation when the field guide is silent.
- Plugin-level config (profile defaults beyond the per-plan context).
- CONPLAN-level annex generation (Levels 3+).

## Status

**v0.1.0** — Initial release.

## License

MIT — see [`LICENSE`](LICENSE).

## Acknowledgements

Built on top of:
- **Joint Publication 5-0, *Joint Planning*** (Joint Chiefs of Staff, 1 December 2020).
- The Claude Code plugin system.
- Inspiration from the [`superpowers`](https://github.com/obra/superpowers) plugin for skill structure.
