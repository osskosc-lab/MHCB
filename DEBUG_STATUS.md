# MHCB Remote Debug Status

## Current blocker

At the time of this submission, the GitHub repository `osskosc-lab/MHCB` was reported by the GitHub API as an **empty repository** (`size: 0`).

The following locally reported commits could therefore not be resolved on the remote:

- `0edcc71aaf17a702a64a46d2c445f4ddb52dcd17`
- `45445370a4b6d4cfe669666354d77ead28b5beff`

This is a **repository publication / synchronization blocker**, not evidence of a scientific or numerical failure in Phase 2A-r1.

## What was and was not debugged here

Verified from the submitted technical report:

- first smoke failure preserved;
- rank-deficiency cause identified as binary `H²` duplicating the intercept;
- outcome-blind zero-variance-column handling was introduced before source freeze;
- second smoke qualified;
- frozen 40-seed run had zero numerical failures;
- G0–G13 passed;
- independent recomputation passed;
- Confirmatory remained untouched.

Not possible from the remote at this point:

- inspect the actual source files at the reported local commit SHAs;
- reproduce unit tests from GitHub;
- inspect local raw CSV artifacts that remain Git-ignored;
- compare local commit history with remote history.

## Required publication step before remote code review

Push or otherwise publish the local source history containing the Phase 2A-r1 implementation to this repository. After the relevant commit objects exist on GitHub, perform a separate remote code audit against the exact source SHA.

Do not freeze or run Confirmatory as part of this publication/debug step.
