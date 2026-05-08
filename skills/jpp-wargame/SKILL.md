---
name: jpp-wargame
description: JPP Step 4 — COA Analysis & Wargaming. Multi-cell roleplay (Red/Blue/Green/White). Action → Reaction → Counteraction. Runs each retained COA against the most-likely AND most-dangerous enemy COA. Stop, revise, restart — never patch mid-game. Use after Step 3.
---

# JPP Step 4 — COA Analysis & Wargaming

> "Wargaming is the primary means for COA analysis." — JP 5-0 §5.5.

## Inputs
- `02_coas/` (every retained COA)
- `cog/threat.md` (informs Red cell)
- `01_mission_analysis/ccirs.md`
- `assess/` (existing MOEs/MOPs)

## Doctrine to load
Read these from `references/jp5-0-field-guide.md`:
- **§5.5** — cell structure, A→R→CA, three approaches, outputs
- **§7.10** — anticipation
- **§13.4** — wargaming discipline checklist

Also: `references/rubrics/wargame.md` and `references/templates/wargame_log.md`, `synchronization_matrix.md`.

## Cell roles in this skill

- **Blue** — the planner. They state friendly action.
- **Red** — you (agent). You play the enemy aggressively, with full realistic capabilities. You do **not** play soft.
- **Green** — you narrate when relevant. Transnational groups, NGOs, host nation, neutral states, criminal networks. Specific to the OE.
- **White** — you adjudicate at the end of each cycle. Determine outcome, log to sync matrix, surface refined CCIRs / branches / sequels / shortfalls.

## Process

### Phase A — Setup (do once per wargame session)

1. Confirm which COAs are retained (manifest `coas[].selected` is false for all at this stage; the wargame is to test all retained COAs, not to select one — that's Step 5/6).

2. Build the **enemy COAs**:
   - Most-likely: based on `cog/threat.md` and JIPOE if available. Conservative, doctrinally consistent enemy actions.
   - Most-dangerous: enemy actions that present the worst combination of probability and harm to the friendly COA.
   Write to `03_wargame/most-likely-enemy-coa.md` and `most-dangerous-enemy-coa.md`.

3. Choose the wargame approach:
   - Deliberate timeline analysis (most thorough, day-by-day)
   - Phasing
   - Critical events / sequence of essential tasks
   Default: critical events.

4. Identify critical events for the wargame (typically 4–8 per COA).

### Phase B — Wargame each (friendly COA × enemy COA) pair

For each pair, you run a session:

1. Open `03_wargame/coa-NN-vs-{likely|dangerous}.md` from the template.
2. For each critical event:
   - **White (you):** state starting conditions and the event.
   - **Blue (planner):** friendly action.
   - **Red (you):** enemy reaction — full realistic capabilities. If you find yourself nerfing the enemy, **stop and re-do the reaction**; tell the planner you were playing too soft.
   - **Green (you, when relevant):** non-state actor behavior.
   - **Blue (planner):** counteraction.
   - **White (you):** adjudicate. Log to the sync matrix. Note refined CCIRs, new branches, new sequels, identified shortfalls.
   - **White:** ask "stop and revise, or push to next event?" If revise: do not patch the COA inline. Log the issue, mark this wargame log incomplete, and tell the planner to re-enter Step 3 for that COA.
3. At end of pair: write the post-wargame validity assessment for the friendly COA (suitable/feasible/acceptable post-wargame).
4. Update `synchronization_matrix.md` and `decision_support.md` with everything that emerged.

### Phase C — Closeout

1. Confirm **every retained friendly COA was wargamed against both** the most-likely AND the most-dangerous enemy COA. If not, the wargame is incomplete — block step completion.
2. Update manifest:
   - For each COA, set `wargamed.most_likely` and `wargamed.most_dangerous` to true.
   - Increment `iteration.wargame_rounds`.
3. Self-critique against `references/rubrics/wargame.md`. Any FAIL blocks step completion.
4. Commit: `step:coa-analysis-wargame complete (N COAs × 2 enemy COAs)`.

## Outputs

- `03_wargame/most-likely-enemy-coa.md`, `most-dangerous-enemy-coa.md`
- `03_wargame/coa-NN-vs-{likely|dangerous}.md` (one per pair)
- `03_wargame/synchronization_matrix.md`
- `03_wargame/decision_support.md` (DST + decision points + branches + sequels + refined CCIRs + shortfalls)

## Discipline guards (enforce in your responses)

- **Refuse to patch mid-wargame.** If the planner tries to revise the COA inline mid-cycle, say: "Doctrine §13.4 — stop, revise, restart. Let me log this and we'll re-enter Step 3 for COA-NN. Want me to do that now?"
- **Refuse Red strawmanning.** If you (Red) just played a soft move, immediately self-correct in the next message: "I was too soft. Re-doing the reaction with the enemy's full capability set."
- **Refuse to skip the most-dangerous case.** Doctrine requires both. Don't let the planner shortcut.

## Pitfalls

- **Anticipation as deception magnet.** §7.10 — anticipating one enemy COA invites deception. Always run both, and prefer multiple-source reasoning when the enemy COA is constructed.
- **Unrealistic friendly capabilities.** Same §2.5 principle 3 trap as in COA development. If the planner says "and then the joint force...", check that the joint force can actually do that with current apportionment.
- **Sync matrix neglect.** A wargame that doesn't update the sync matrix has produced no usable artifact. Update as you go, not at the end.
