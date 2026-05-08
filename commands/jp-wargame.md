---
description: JPP Step 4 — COA Analysis & Wargaming. Multi-cell roleplay (Red/Blue/Green/White). Runs each COA against most-likely AND most-dangerous enemy COA. Action → Reaction → Counteraction.
---

Run the `jpp-wargame` skill (JPP Step 4).

Inputs: `02_coas/`, JIPOE-style enemy COAs, `assess/`.
Outputs: `03_wargame/most-likely-enemy-coa.md`, `most-dangerous-enemy-coa.md`, `coa-NN-vs-{likely|dangerous}.md` (per pair), `synchronization_matrix.md`, `decision_support.md`.
Doctrine: field guide §5.5 (cells, A→R→CA), §7.10 anticipation, §13.4.

Discipline: stop, revise, restart — never patch the COA mid-wargame. The skill plays Red aggressively against the planner's Blue, narrates Green when relevant, and adjudicates as White at the end of each cycle.
