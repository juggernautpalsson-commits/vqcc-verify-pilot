# VQCC Verify Pilot

Runs the **official invsqrt verifier** from Google's Verifiable Quantum
Circuit Compilation competition on one adopted public leg, using a free
GitHub Actions runner (4 vCPU / 16 GB) instead of a local machine.

Competition: <https://www.kaggle.com/competitions/google-verifiable-quantum-circuit-compilation>

## What this repo is

A pilot for offloading CPU-heavy leg verification to GitHub Actions.
It verifies **adopted public legs only** — circuits published by other
competitors under open licences. It contains no original research code
and no submission packages.

## Layout

| Path | What it is |
| --- | --- |
| `.github/workflows/verify-pilot.yml` | The workflow: Python 3.13 + numpy/scipy, then the official verifier on the committed leg. Manual trigger only. |
| `verifiers/invsqrt/` | The competition's official invsqrt verifier (`verify_submission_invsqrt.py`), verbatim from the competition data. |
| `kickmix/kickmix.so` | The competition's `kickmix` simulator module (compiled CPython 3.13 extension, Linux x86-64), verbatim from the competition data. |
| `legs/invsqrt.kmb` | One adopted public invsqrt leg (binary kickmix circuit). |
| `LICENSE` | Apache License 2.0, as shipped with the competition code. |

## How to run it

1. Open the **Actions** tab.
2. Select **verify-pilot** in the left sidebar.
3. Click **Run workflow** (default branch), then **Run workflow**.

The run takes roughly 15–30 minutes. No secrets or extra setup are
needed — everything the run needs is committed in this repo.

## How to read the result

When the run finishes, the **Artifacts** section at the bottom of the
run page has `invsqrt-verification`, containing:

- `result.json` — the verifier's JSON summary: `status` (`PASS` or
  `FAIL`) and the measured score and circuit metrics.
- `verify.log` — the verifier's stderr log (useful if the run fails).

## Licence and provenance

The verifier and the `kickmix` module are the competition organisers'
code, distributed under the Apache License 2.0 (see `LICENSE`). The
committed leg is an adopted circuit from a public Kaggle notebook,
published under Apache-2.0. This repo adds only the workflow file and
this README.
