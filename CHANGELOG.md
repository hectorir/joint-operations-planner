# Changelog

## [0.1.0] — 2026-05-07

Initial release.

### Added
- Plugin scaffolding (`.claude-plugin/plugin.json`, README, LICENSE).
- Umbrella agent `joint-planner` for routing.
- 16 slash commands: `/jp`, `/jp-status`, `/jp-plan`, `/jp-coach`, `/jp-critique`, `/jp-generate`, and one per JPP step (`/jp-initiation`, `/jp-mission-analysis`, `/jp-coa-development`, `/jp-wargame`, `/jp-coa-comparison`, `/jp-coa-approval`, `/jp-plan-development`), plus `/jp-cog`, `/jp-risk`, `/jp-assess`.
- 14 skills mirroring the slash commands.
- Doctrine reference: JP 5-0 Practitioner Field Guide.
- Templates for every artifact (mission statement, COA, wargame log, sync matrix, comparison matrix, decision, CONOPS, OPORD 5-paragraph, risk assessment, assessment plan, CCIRs, assumptions, COG critical factors, manifest seed).
- Practitioner checklists §13.1–§13.6.
- Doctrinal rubrics for `/jp-critique` (mission analysis, COA, COG, wargame, plan, risk).
- Worked example: `examples/exercise-pacific-cyclone` (fictional UNCLASSIFIED HADR scenario).
- Plan-dir contract: `manifest.yaml` schema, numbered step folders, git-versioned by default.
- Plan scope: Levels 1 (Commander's Estimate) and 2 (BPLAN). No CONPLAN/OPLAN annexes in v1; no TPFDD.
- UNCLASSIFIED-only guardrail in agent prompts and README.
