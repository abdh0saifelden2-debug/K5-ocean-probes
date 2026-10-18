# Ocean probes — double diffusion at the ice–ocean interface (salt + temperature)

Where the two-clocks framework meets **seawater**: cold-fresh meltwater over
warm-salty ocean, two buoyancy-active scalars with a 100× molecular-diffusivity
contrast (`Le = 100`), and what a scalloped ice wall does to that system.

Closely related ocean-facing work that runs on *ice-sheet* geometry — the §G.3
**ocean-intrusion** RTN (verified directional at the grounding line) and the
§H.1.2 intrusion clock, plus the CATS2008 tide loader — sits in
**`K2-subglacial-cavity`** (see Provenance below). The transport-memory result
(RESULT 13: `τ_c` identical for heat and salt) is in **`K1-two-clocks-theory`**.

## What was found so far

- **[VERIFIED, honest negative]** Candidate 2 — the pre-registered salt-finger
  hump is **absent**: `Nu_T(R_ρ)` decreases monotonically (1.44 → 0.73 across
  `R_ρ = 0.5 → 10`); `R_ρ ≈ 2` is *not* a maximum in this 2-D forced penalized
  regime. [`REPORT_CANDIDATE2.md`](REPORT_CANDIDATE2.md), Fig 48
  (`run_candidate2.py`).
- **[VERIFIED]** The diffusivity contrast *does* show up robustly: `Nu_S ≫ Nu_T`
  (salt transported far more efficiently than heat) and **counter-gradient** heat
  flux at strong stabilisation — another flux-space signature down-gradient
  K-theory cannot produce.
- **[VERIFIED structural, §D.2]** A scalloped wall on the same double-diffusion
  solver: phase-binned `Nu_T` heterogeneity amplified (5.3 → 67 peak-to-trough),
  wall-coherent variance fraction `η²` 0.09 → **0.89** (phase-locked, with a
  dominant 2nd harmonic), and *both* double-diffusive regimes (enhanced 93% /
  suppressed 7% of the wall) **coexist in one geometry** — local Turner-ratio
  mixing. [`REPORT_DOUBLEDIFF.md`](REPORT_DOUBLEDIFF.md), Fig 50 (GPU).
- **[VERIFIED, RESULT 13 — reported in `K1-two-clocks-theory`]** the transport
  memory time `τ_c` is identical for heat and salt despite `Le = 100`: the clock
  belongs to the turbulence, not the scalar.

## What remains a HYP

- **Salt fingers in realistic regimes [HYP]** — the absence of the `Nu_T` hump
  may be an artifact of 2-D + penalization + forcing; 3-D unforced
  double-diffusive staircases remain untested here.
- **Real ice-shelf relevance [HYP]** — whether scallop-locked regime mixing
  (§D.2) shapes melt under actual ice shelves (e.g. staircase observations under
  George VI) is not tested against ocean data.
- **§G.3 threshold [HYP / LIT]** — RTN as the quantitative criterion for warm
  ocean water intruding under grounded ice leans on literature closures; the
  claim itself lives in `K2-subglacial-cavity`.

## What is pending

- A 3-D double-diffusion run (the solver family is GPU-ready; the cupy test
  harness lives in the monorepo archive).
- Testing the §D.2 regime-coexistence prediction against oceanographic
  microstructure / ice-shelf cavity observations.
- Coupling the double-diffusive `Nu_S ≫ Nu_T` asymmetry into the §G.6 melt-rate
  phenomenology (currently local-flux-only).

## Contents

- `run_candidate2.py` — Candidate 2 `R_ρ × closure` sweep (Fig 48).
- `scallop_doublediff.py` — §D.2 scalloped-wall double-diffusion regime mixing
  (Fig 50).
- `subglacial/` — the double-diffusion solver (`candidate2_doublediff.py`) and
  roughness-feedback solver (`candidate3_roughness_feedback.py`), vendored from
  the cavity library so this repo is import-clean on its own (see `AUDIT.md`).
- Reports: [`REPORT_CANDIDATE2.md`](REPORT_CANDIDATE2.md),
  [`REPORT_DOUBLEDIFF.md`](REPORT_DOUBLEDIFF.md).
- `figures/` — Figs 48, 50. `tests/` — `test_candidate2.py`,
  `test_doublediff_scallop.py`.

## Quick start

```bash
python3 -m venv .venv && . .venv/bin/activate
pip install -r requirements.txt
python run_candidate2.py
python -m pytest            # 24 passed
```

## Provenance

Split out of the **K** monorepo, partitioned by claim cluster:

| repository | claim cluster |
|---|---|
| `K1-two-clocks-theory` | observation, two-clocks theory, closure benchmarks |
| `K2-subglacial-cavity` | cavity DNS, real-bed validation, field-analysis validation |
| `K3-scallop-migration` | scallop instability family, channelisation |
| `K4-swirl-vortex` | atmospheric vortex application |
| `K5-ocean-probes` *(this repo)* | ice–ocean double diffusion |

The pristine monorepo was snapshotted **before** any edit:
`K-monorepo-archive.tar.gz`, SHA-256
`ef637ff55f912a5d1404f677429f9429eccc8102a8cab23cee79cf055bbf1220`
(`K-monorepo-archive.sha256`). The cross-repo claim ledger (`FUTURE_WORK.md`)
and paper outline are deliberately **not** copied here — they live only in that
archive. `AUDIT.md` records the AST dependency audit that decided this split
(reproduce it with [`K-audit` v1.0](https://github.com/abdh0saifelden2-debug/K-audit/tree/v1.0)).
