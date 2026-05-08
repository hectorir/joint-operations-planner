---
name: jpp-coa-development
description: JPP Step 3 — COA Development. Produces 2–4 distinguishable, valid courses of action. Each COA file is self-contained (sketch + who/what/where/when/why/how + COG focus + 5-validity-test results). Use after mission analysis is complete.
---

# JPP Step 3 — COA Development

## Inputs
- `01_mission_analysis/` (especially mission statement, tasks, CCIRs, COGs, COA evaluation criteria)
- `cog/friendly.md`, `cog/threat.md`
- `context.md`

## Doctrine to load
Read these from `references/jp5-0-field-guide.md`:
- **§5.4** — required components, the 5 validity tests
- **§7.2** — objectives, end state, effects, tasks
- **§7.5** — LOOs vs LOEs
- **§7.6** — decisive points
- **§7.7** — direct vs indirect approach
- **§7.9** — arranging operations (simultaneity, depth, timing/tempo, phasing, branches/sequels, operational pause)
- **§9** — defeat/stabilization/competition mechanisms
- **§13.3** — COA validity gate

Also: `references/rubrics/coa.md` and `references/templates/coa.md`.

## Process

1. **Scope COA generation.** Ask the planner: how many COAs to draft? Default is 3 — fewer than 3 makes Step 5 weak; more than 4 dilutes the staff effort. Each COA must be **distinguishable** (§5.4.1 #4) — materially different in at least one of: focus/main effort, scheme of maneuver, sequencing, mechanism, task org, use of reserves.

2. **For each COA**, work through the template at `references/templates/coa.md`:
   - Sketch (one paragraph, plain language).
   - Who/What/Where/When/Why/How.
   - COG and decisive points focus (direct or indirect approach; which CVs).
   - Force employment mechanism (defeat/stabilization/competition + specific verb).
   - Decision points and assessment process.
   - End-state criteria.
   - Run the **5 validity tests** in the file's table — score `pass`/`warn`/`fail`/`pending` with rationale.

3. **Write each COA to its own file:** `02_coas/coa-NN-<short-kebab-name>.md` with NN zero-padded (`coa-01`, `coa-02`, …).

4. **Update manifest.** Add each COA to the `coas[]` array with id, short_name, file, validity, wargamed (both false), selected (false).

5. **Reject invalid COAs.** A COA that fails any of the 5 tests is not retained for Step 4. Tell the planner clearly: "COA-02 fails the feasibility test — the proposed deployment timeline exceeds available strategic lift. Drop, modify, or replace."

6. **Self-critique gate.** Walk `references/rubrics/coa.md` for each retained COA. Any FAIL means re-work or drop.

## Outputs

- `02_coas/coa-01-<short-name>.md`, `coa-02-<short-name>.md`, … (one file per retained COA)
- `manifest.yaml` updated with `coas[]`

## Commit message

`step:coa-development complete N COAs retained` (or `in-progress`)

## Pitfalls

- **Cookie-cutter COAs.** If COA-2 is "COA-1 but slower" or "COA-1 but more forces," it fails distinguishability. Force a real difference in approach.
- **Inventing forces.** COAs use currently available capabilities (§2.5 principle 3). If a COA assumes a future capability, that's a feasibility fail.
- **Burying the COG.** Every COA should name how it protects the friendly COG and acts on the threat COG (or its critical vulnerabilities for an indirect approach). If absent, that's a §7.6 / §8 gap.
- **Mechanism mismatch.** Using "destruction" verbs in a stabilization scenario; using "compel" in a force-on-force scenario. Match the mechanism to the context per §9.
- **No main effort.** Designate it as soon as possible; it can shift across phases (§5.8.1) but cannot be absent.
