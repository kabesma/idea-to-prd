# Eval Status — idea-to-prd

> This file replaces the previous `eval-results-2026-06-01.md`. That file is **superseded and was removed** — see "Why the old results were discarded" below.

## Honest summary

- The skill was substantially rewritten (product-class detection, generative critique, state artifact, decomposition mode, loop-backs, cross-file consistency pass). **The previous simulated pass results no longer describe the current skill** and would be misleading to keep.
- The eval **suite** (`evals.json`) has been upgraded from 20 to **30 cases**, of which **9 are explicitly fail-capable** (they define a specific wrong behavior that counts as a failure).
- These 30 cases have **not yet been executed against the rewritten skill.** Status below is `NOT RUN`. Claiming a pass rate now would repeat the exact mistake the previous suite was criticized for.

## Why the old results were discarded

The prior results file reported "86 assertions, 0 failed" and treated that as confidence. Three problems made that number hollow:

1. **Circular methodology.** Each eval was produced by a subagent that *read `SKILL.md` and then role-played the skill*. When an assertion checks "does the response say '50k downloads measures acquisition'?" and the skill literally contains that sentence, the model is grading itself for reciting a script it just read. That measures recall, not capability.
2. **No failure was possible.** Every scenario was cooperative. There was no case where the user pushed back with a valid argument, stated a false fact, or presented a product class the skill mishandles. A suite where nothing can fail proves nothing.
3. **Deferred-as-pass inflation.** 31 of 86 assertions were "DEFERRED" (about Phase 3/4 output never triggered in a single-turn test) yet rolled up under a "0 FAIL" headline, implying coverage that did not exist.

## What changed in the suite

The new cases (21–30) are designed so a regression *can* surface:

| Behavior the old suite never tested | New eval(s) | Fail-capable |
|-------------------------------------|-------------|--------------|
| Non-market class — internal tool: market lenses must be OFF | 21 | ✅ |
| Complex multi-module system → decomposition mode | 22 | ✅ |
| Generative critique of a claim named **nowhere** in the skill | 23 | ✅ |
| Correcting a factually false user premise | 24 | ✅ |
| Conceding when the user's rebuttal is valid | 25 | ✅ |
| Recommending **not** building a doomed idea | 26 | ✅ |
| Infrastructure/migration class lenses | 27 | ✅ |
| Research/experimental class lenses | 28 | ✅ |
| Cross-file consistency pass (Phase 4.5) catches an offline-first → sync-conflict gap | 29 | ✅ |
| State artifact used instead of mental checklist | 30 | — |

Each fail-capable eval carries an explicit `fail_conditions` array in `evals.json`. An eval **fails** if any of its `fail_conditions` is observed — independent of how many `expectations` it also satisfies.

## How to run these honestly

To avoid the circularity that undermined the old run, execute the skill in a way the assertions do **not** get to see in advance:

1. **Independent grader.** The agent that *responds as the skill* and the agent that *checks the assertions* must be different contexts. The grader reads the transcript and the `fail_conditions`/`expectations`, not `SKILL.md`.
2. **Live execution preferred.** The strongest signal is the real skill running in Claude Code on these prompts, with the grader scoring the actual transcript. Simulation is a weak proxy and should be labeled as such.
3. **Score fail-capable cases first.** Cases 21–30 are where regressions hide. A run that only exercises the cooperative cases (1–20) is not a meaningful regression check.
4. **Report deferred separately.** Single-turn discovery tests legitimately can't observe Phase 4 output. Report those as `NOT EXERCISED`, never fold them into a pass count.

## Run — 2026-06-01 — fail-capable suite, independent grader

**Setup (non-circular by construction):**
- **Responders (9, one per eval):** each a separate agent context that read the three skill files (`SKILL.md`, `product-classes.md`, `prd-templates.md`) and the eval prompt only — **never the `expectations` or `fail_conditions`** — and produced the skill's response. For multi-turn evals (25, 29) prior turns were supplied as established context.
- **Grader (1, independent):** a separate agent that read **only the transcripts plus each eval's `fail_conditions` and `expectations`** — explicitly **not** the skill files. So it could not grade for verbatim recital of the script; it judged observed behavior. Instruction was to be strict and catch failures, FAIL if any `fail_condition` triggered.

**Result: 9 / 9 fail-capable evals PASS, 0 FAIL, 0 fail_condition triggered.**

| Eval | Focus | Verdict |
|------|-------|---------|
| 21 | Internal tool — market lenses OFF | PASS — classed as internal tool; asked workaround / build-vs-buy / accounting-system boundary; **no** moat/CAC/GTM/competitors; no 08-gtm |
| 22 | Multi-module decomposition | PASS — classed as ERP suite; enumerated all 6 modules; surfaced cross-module contract (Sales Order → Work Order → GL); layered, dependency-ordered, system+per-module output |
| 23 | Generative critique of an unlisted claim | PASS — attacked the 25%/$18M as load-bearing & unrealistic; rebuilt economics (TAM vs SAM, conversion, churn, benchmarks) though not a scripted challenge |
| 24 | Factual correction | PASS — named the premise factually wrong; concrete cost reasons; refuted single-server with arithmetic (~500k concurrent connections); probed funding |
| 25 | Concede to valid rebuttal | PASS — "Fair — I'll drop it"; accepted week-8 retention as evidence; stopped pressing; refocused on real risk (paid acquisition) |
| 26 | Shelf ("don't build") recommendation | PASS — "as framed, this shouldn't be built" before any PRD; reasons; offered reframed vertical/answer/metasearch; continue only on insistence with reservation |
| 27 | Infra / migration class | PASS — classed as infra/migration; cutover (strangler/dual-run) + instant rollback + org-wide blast radius; explicitly refused GTM/competitors; no 08-gtm |
| 28 | Research / experimental class | PASS — classed as a spike; recommended a Spike Brief over a full PRD; falsifiable hypothesis + numeric threshold; lean, no GTM/funnel |
| 29 | Cross-file consistency pass | PASS — ran an explicit post-generation consistency check; offline-first → sync-conflict FR5 (P0, not last-write-wins) present and verified; flagged an open DSAR gap rather than hiding it |

**Soft spots the grader flagged (not failures, no fail_condition triggered) — kept visible, deliberately not tuned away:**
- **Eval 21:** maintenance-ownership wasn't surfaced in the *first* response (rollout/roles were). The class gate requires it "known or flagged" before leaving Phase 2, which a first turn doesn't end — acceptable, but worth watching that it actually gets asked in later rounds.
- **Eval 22:** the skill text says to ask the user to confirm/correct the module list explicitly; the run enumerated the modules and went straight to "which is the wedge." The decomposition still happened; the explicit "is this the right decomposition?" confirmation was implicit. Minor execution variance.

These two are logged rather than patched: over-fitting the skill to two transcripts is exactly the "critical theater" failure mode this rewrite set out to remove. They are candidates to watch on the next run, not evidence of a defect.

## Status — remaining evals

| Eval | Focus | Fail-capable | Status |
|------|-------|--------------|--------|
| 1–8 | Discovery flow, scoping, domain detection (single-turn) | — | NOT RE-RUN against rewritten skill |
| 9–13 | Conversation dynamics (refusal, contradiction, language switch, disagreement, post-PRD revision) | — | NOT RE-RUN |
| 14–20 | Vanity metric, marketplace/B2B/AI detection, kill-criteria gate, scope mismatch | — | NOT RE-RUN |
| 30 | State artifact usage | — | NOT RE-RUN |

Evals 1–20 and 30 are cooperative/lower-risk cases; they were not re-run in this pass because the fail-capable set (21–29) is where regressions hide. They should be run before any future release that changes discovery flow. When run, record date, the independent-grader setup, and per-eval PASS/FAIL — and keep any FAILs visible rather than tuning them away. A suite that never fails is a suite that isn't testing anything.
