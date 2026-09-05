# MHCB Phase 2A-r1 Amendment Pilot Audit — Current Report

**Status:** AMENDMENT_READY_TO_FREEZE  
**Scope:** Human freeze review only. This report does **not** freeze or authorize Confirmatory execution.

## Provenance

- Parent Pilot commit (local source history): `8a90951686a7bab76d2775d9f2366169909bf471`
- Amendment source commit (local source history): `0edcc71aaf17a702a64a46d2c445f4ddb52dcd17`
- Current audit commit reported by local run: `45445370a4b6d4cfe669666354d77ead28b5beff`
- Amendment Pilot seeds: 40, IDs `0–39`
- Base seed: `20280813`
- Confirmatory cohort: untouched

> Important: the commit SHAs above were reported by the local Codex run. At submission time, the GitHub remote was still empty, so those commits were not yet present on GitHub.

## Validation

- Unit tests: **35 passed in 1.62s**
- First preserved smoke: **IMPLEMENTATION_FAILURE**
  - 800 rank-deficient rows
  - cause: binary-history `H²` duplicated the intercept
- Outcome-blind zero-variance-column handling added before source freeze
- Second smoke: **SMOKE_IMPLEMENTATION_QUALIFIED**
  - 928 rows
  - 464 cells
  - zero numerical failures
  - no scientific inference

## Frozen gates

| Gate | Criterion | Result |
|---|---|---|
| G0 | Provenance integrity | PASS |
| G1 | Null false-positive control | PASS |
| G2 | Positive-control reproduction | PASS |
| G3 | State-completeness response | PASS |
| G4 | Reset-strength response | PASS |
| G5 | Full-state/full-reset extinction | PASS |
| G6 | Irreducible-floor survival | PASS |
| G7 | Joint-mediator compatibility | PASS |
| G8 | Seed-level robustness | PASS |
| G9 | Independent recomputation | PASS |
| G10 | Path-specific intervention discrimination | PASS |
| G11 | State-order robustness | PASS |
| G12 | Nonlinear false-negative control | PASS |
| G13 | Confirmatory-cohort isolation | PASS |

## Path-specific intervention findings

- `state_misspecified`
  - none: 0.9853
  - cut_X: 0.0219
  - cut_C: 0.9949
  - cut_XC: 0.0251
- `incomplete_reset`
  - none: 0.8964
  - cut_X: 0.9013
  - cut_C: 0.0248
  - cut_XC: 0.0262
- `irreducible`: approximately 0.643–0.653 across cuts
- `mixed`
  - none: 2.5492
  - cut_X: 1.5481
  - cut_C: 1.6514
  - cut_XC: 0.6587

The intervention equations were structurally distinct and were not implemented as post-hoc outcome scaling.

## State-order robustness

Strong-first was favorable at partial state budgets:

- strong-first mean curve: 0.3797
- weak-first mean curve: 0.6205

However, full-state `state_misspecified` means converged to 0.0315–0.0383 and the registered mechanism classification survived all four preregistered state orders.

Interpretation: intermediate MHCB curves are representation-relative; the registered full-state mechanism classification was order-robust in this synthetic audit.

## Nonlinear false-negative controls

Primary additive OLS `B_H` was null-like:

- `interaction_only`: 0.0278–0.0354
- `nonlinear_history`: 0.0416–0.0575

Secondary held-out nonlinear diagnostic `D_NL` was strongly positive:

- `interaction_only`: 0.4976–0.5074
- `nonlinear_history`: 0.4227–0.4370

All corresponding seed-level `D_NL` values were positive and all registered 95% intervals excluded zero.

Correct audit interpretation:

`PRIMARY_LINEAR_ESTIMAND_NOT_SENSITIVE`

not:

`NO_HISTORY_EFFECT`

## Null and irreducible controls

- Maximum primary null cell mean: 0.03135
- Primary practical-null threshold: 0.12
- Maximum secondary null cell mean: 0.000305
- Secondary tolerance: 0.01
- Irreducible joint-cut means across orders: 0.6462–0.6586
- Seed minima: 0.5941–0.6102
- Numerical failures in frozen 40-seed run: 0
- Maximum primary condition number: 5.56
- Maximum nonlinear condition number: 6.32

## Precision

- `B_H` 95% CI width
  - median: 0.01698
  - p95: 0.02921
  - max: 0.04487
- `D_NL` 95% CI width
  - median: 0.01808
  - p95: 0.05349
  - max: 0.08116

## Independent recomputation and integrity

- 6,264 summaries independently recomputed
- standard deviations, seed ranges, CIs and gate inputs matched
- G9: PASS
- 9 Amendment artifacts verified
- 8 parent-Pilot artifacts remained verified
- Confirmatory rows: 0
- Confirmatory output directory: absent
- Confirmatory config SHA256:
  `dd6030a82f9be930c95700e548ddfdb059dbcd6e34c68820334459dc01ba8dfd`
- freeze tags: none

## Adversarial findings that remain claim boundaries

1. `cut_XC` remains oracle-like.
2. Reset and mediator cuts are partly redundant.
3. State completeness and reset are not orthogonal in every DGP.
4. Strong-first materially improves partial-state curves.
5. Mixed and irreducible converge after all mediated paths are removed.
6. A single endpoint is non-diagnostic; the response surface is required.
7. `D_NL` covers only its fixed preregistered basis.
8. Mediator-level distribution moments were not preserved as raw metrics.
9. Paired seed contrasts did not use common random numbers.

## Current decision

`AMENDMENT_READY_TO_FREEZE`

This means the amended synthetic design is ready for **human freeze review only**.

It does **not** establish universal or real-world causal identifiability, does not prove irreducible historical causation in unknown systems, and does not authorize Confirmatory execution.
