# UrbanRay — Unified AI Decision Engine

**NEW: [START_HERE.md](START_HERE.md)** — Open the complete offline app at **`outputs/unified_decision_engine/dashboard/UrbanRay_AI_Explorer_OFFLINE.html`**. This builds on and preserves the existing geometry-aware regression and dedicated hotspot models, adds one shared inference/decision interface and model disagreement/review flags, and keeps the existing blue/black visualization design. Details and verification: [UNIFIED_DECISION_ENGINE_REPORT.md](UNIFIED_DECISION_ENGINE_REPORT.md). **59 tests passed.** This is simulated evidence, not field validation or a new untouched benchmark. Verify Veritas eligibility before submitting an extension of pre-existing work.

---

# UrbanRay — Geometry-Aware AI and Dedicated Reflection-Hotspot Model (Research Edition)

**Start here:** [GEOMETRY_AI_UPGRADE_REPORT.md](GEOMETRY_AI_UPGRADE_REPORT.md) and open **`outputs/geometry_ai_upgrade/dashboard/UrbanRay_AI_Explorer_OFFLINE.html`** for the fully offline enhanced dashboard.

This package adds a trained neighboring-building geometry-aware reflection-residual AI, a specialist top-K wall-hotspot model, a controlled no-geometry ablation, full comparison tables, new tests, and a fail-closed real-world validation preflight. **51 tests passed**, and the enhanced dashboard was exercised in Chromium without page errors. On the *previously inspected* June 23 simulator test: old AI 3.63 W/m² MAE, geometry AI 3.08, specialist 3.02; specialist top-20 reflection exposure captured 85.9% vs old 81.1%. These are **simulated physics targets, not independent observed roof temperatures**. The smoke comparison shows the AI is **slower** than the sparse physics reference, and authentic paired AI-vs-satellite validation is **not complete**.

```bash
python -m pip install -r requirements.txt
python -m pytest -q tests
python train_geometry_ai.py
python build_ai_dashboard.py --model outputs/geometry_ai_upgrade/regression_surrogate.joblib --heldout outputs/geometry_ai_upgrade/retrospective_heldout_predictions_SIMULATED.csv --output outputs/geometry_ai_upgrade/dashboard
python observational_preflight.py
python verify_checksums.py
```

The original 2026 Veritas competition rules described in this archive prohibited extending projects made earlier than the event. **This upgraded archive does not on its own establish eligibility.**

---

# UrbanRay — Real-World Advantage Research Upgrade (15 November 2026)

**Latest research edition:** `outputs/ai_upgrade/UrbanRay_AI_Explorer_OFFLINE.html` opens directly in a browser and now includes a highlighted AI-reflection map, actual modeled **solar heat** (kWh/day) roof-screening calculations, a strict held-out **reflection-hotspot selection** benchmark and an explicitly labeled **physics-only** Landsat observation panel. It does NOT claim measured AI roof cooling, better rooftop project choices over the baseline, or a faster AI model.

**Start with:** [`REAL_WORLD_UPGRADE_REPORT.md`](REAL_WORLD_UPGRADE_REPORT.md) for results, validation steps and limitations. The locked split selects reflection-exposed facades better than a direct-only rule (top 20: **81.14% vs 11.46%** of the simulator's maximum top-20 exposure), but rooftop priority selection shows no added AI advantage at K=3,5,10. All figures are simulator-relative, except the separately labeled physics-only Landsat diagnostic.

```bash
python -m pip install -r requirements.txt
python -m pytest -q tests
python decision_benchmark.py
python reflection_hotspot_audit.py
python build_ai_dashboard.py
```

**Competition eligibility:** The Veritas AI 2026 rules prohibit extending work from before the hackathon. This codebase contains an earlier project, so this upgrade alone is **not** submission eligibility evidence. Confirm with organizers before any attempted entry: <https://highschoolhackathon.org/briefs>.

---

# UrbanRay — AI Reflection-Correction Research Edition (15 November 2026)

**Open the demo first:** `outputs/ai_upgrade/UrbanRay_AI_Explorer_OFFLINE.html` — a self-contained HTML dashboard with AI/physics comparison, real NYC geometry, scenario rankings, feature importance, and a 2D fallback when 3D/WebGL is unavailable.

**Read the scientific/eligibility warning:** `AI_UPGRADE_REPORT.md`. The Veritas AI hackathon requires ALL submitted project code to be written during its 48-hour window and explicitly disallows extending earlier projects. Adding these features does not establish hackathon eligibility. The released Climate brief was not independently available within this package, so do not claim guaranteed alignment with its particular prompt.

## AI-first quick start

```bash
python -m pip install -r requirements.txt
PYTHONPATH=src python -m pytest -q tests
# Re-create the locked split comparison, with model selection on validation only
python train_reflection_residual.py --faces outputs/historical_ml/physics_training_faces.csv --out outputs/ai_upgrade/reflection_residual
# Rebuild the offline interactive explorer
python build_ai_dashboard.py
```

To run the three-way physics/AI/no-reflection integration on the clearly **synthetic test weather** bundled for software tests:

```bash
python run_physics_plus.py --weather-csv outputs/ai_upgrade/SMOKE_ONLY_daylight_2hour_weather.csv --output outputs/ai_upgrade/SMOKE_ONLY_COMPARE --radiation-mode compare --rays 1 --shadow-samples 1 --warmup-hours 0 --hours 2 --bounces 2 --no-face-csv
```

The chosen AI is a gradient-boosted **reflection-residual model**: it estimates the missing inter-reflection absorption on top of direct+sky shortwave input. On the test date/spatial blocks, its MAE against SIMULATOR outputs is **3.635 W/m²**, compared with **7.898 W/m²** for the direct+sky baseline. This is **not** verified urban temperature prediction. On the synthetic short-run test, the AI is **slower** than the sparse shortwave reference; don't describe the project as an AI accelerator.

**Documents:** `ONE_PAGE_AI_PROJECT_BRIEF.md` (concisely written scientific summary); `DEMO_SCRIPT_2MIN.md` (optional walkthrough); `AI_UPGRADE_REPORT.md` (full methods, measured scores, limitations, citations); `UPGRADE_CHANGELOG.md` (changed files); `SCIENTIFIC_STATUS.md` (earlier satellite-validation caveats).

---

## Original archive guide (retained for provenance)

# UrbanRay — Latest Complete Package (15 November 2026)

**One authoritative project bundle.** The latest physics source is **Physics+ v2 integrated into Validation v3**, plus the newer **2025–2026 Landsat date search**, **10-date simulation plan**, and **actual 10-scene exploratory results/audit**.

## Open first

- `UrbanRay_Latest_Colab.ipynb`: notebook for setup, verification, charts, and *optional* new simulations.
- `README.md`: this guide.
- `SCIENTIFIC_STATUS.md`: what the project demonstrates and what remains unverified.
- `outputs/multidate_validation/audit/AUDIT_REPORT.md`: independent arithmetic and cautions for ten observed satellite scenes.

## Quick start (local Python or Colab terminal)

```bash
python -m pip install -r requirements.txt
PYTHONPATH=src python -m pytest -q tests
python UrbanRay_Run_10Date_Validation.py --all --dry-run
```

The project does **not** need more Earth Engine exports to display its currently archived validation results. To search for further overpasses, paste **only** `earth_engine/UrbanRay_Find_Matching_Landsat_Dates.js` into the **Earth Engine JavaScript Code Editor**, **not** a Python notebook.

## Current evidence

- Municipal NYC geometry: 88 documented buildings in `data/nyc_88_source.geojson`, with 2,082 simplified modeled surface patches.
- Archived real-weather-based multi-day physics simulation from June 2025 in `outputs/historical_ml/` (model input weather hashes are recorded, but **raw historical weather is NOT included**).
- Trained simulator surrogate and its held-out simulation-relative scores in `outputs/ml_holdout/`.
- Independently sourced Landsat exports: 150 candidate scenes, 44 shortlisted scenes, and 1,104 qualifying 30m output-grid rows, stored as the three `urbanray_*_2025_2026.csv` files at project root.
- Ten already-completed scene-level exploratory satellite-to-model comparisons in `outputs/multidate_validation/`, including five earlier 2025 development scenes and five 2026 held-out scenes.
- Held-out scene-level raw MAE **3.526 °C**; after additive correction learned from the five development scenes, **2.341 °C**. This is exploratory *proxy-versus-retrieval disagreement*, **not verified individual-roof temperature accuracy**. See audit limitations.

## Common workflows

**Explore existing 10-date results**

```python
import pandas as pd
print(pd.read_csv('outputs/multidate_validation/scene_level_EXPLORATORY.csv').to_string(index=False))
```

**Reproduce ray/geometry unit checks**

```bash
PYTHONPATH=src python -m pytest -q tests
```

**Inspect the selected 10 historical overpass dates, before running**

```bash
python UrbanRay_Run_10Date_Validation.py --all --dry-run
```

**Run one selected observation date with actual external historical weather**

```bash
python UrbanRay_Run_10Date_Validation.py --dates 2025-04-23
```

This re-downloads missing Open-Meteo gridded weather with source provenance, runs the Physics+ model with 48-hour warm-up and 16 rays, and compares the resulting face temperatures to the already-provided Landsat measurements. **Computationally expensive; internet is required.** The ten-date summarized result is already archived, so a rerun is *optional*, not required to see existing metrics.

**Retrain the AI on the included historical face-level simulation dataset**

```bash
python train_surrogate.py --faces outputs/historical_ml/physics_training_faces.csv --out outputs/ml_retrained
```

**Launch a fresh historical simulation**

```bash
python fetch_weather_range.py --start 2025-06-18 --end 2025-06-25 --out data/nyc_weather_2025.csv
python run_physics_plus.py --weather-csv data/nyc_weather_2025.csv --warmup-hours 48 --hours 96 --rays 8 --output outputs/new_historical_run
```

## Contents

- `src/`, `run_physics_plus.py`, `fetch_weather_range.py`: current 88-building thermal/shortwave/longwave implementation.
- `train_surrogate.py`: AI trained to predict physics-simulator shortwave targets (not measured roof temperatures).
- `validate_landsat_pixels.py`, `evaluate_scene_holdout.py`, `UrbanRay_Run_10Date_Validation.py`: current satellite comparison and preselected dates.
- `earth_engine/`: one current date-search + filtered-pixel export (5 K exploratory threshold). Previous 3 K and incompatible-projection scripts intentionally excluded.
- `data/`: real geometry and archived ray test inputs.
- `tests/`: included unit tests; synthetic fixture CSVs are for tests only.
- `outputs/historical_ml/`: historical physics outputs, including large face-level file and visualizations.
- `outputs/ml_holdout/`: trained surrogate, held-out predictions and audit.
- `outputs/historical_sensitivity/`, `outputs/ray_convergence_multi_seed/`: sensitivity and numerical repeatability.
- `outputs/multidate_validation/`: observed-vs-modeled summary, heldout correction and audited figures.
- `CHECKSUMS_SHA256.json`: checksums for all package files except the checksum manifest itself.

## Completeness and limitations

This bundle includes **everything currently available here needed to read/reuse the latest source, observed Landsat exports, trained AI, and reported summary results**. It does **not** contain the raw Open-Meteo weather CSV/API responses for all ten satellite dates, the full per-date face-temperature outputs, or all pixel-level matches from the 10-date run; those were not included in the submitted multi-date results ZIP. Therefore, its ten-date simulation histories **cannot be independently rerun offline**. The supplied downloader/re-run script supports reproducing them when external weather is accessible. The 2026 test dates were subsequently inspected; do not claim further tuning on these scenes would be a pristine held-out test.

Data and geometry choices are model approximations. Landsat native thermal resolution (~100 m) is coarser than its 30 m product grid; rows in a single scene are correlated. No measured individual-building roofing material data; no ground-observed rooftop temperature series. Existing-roof observations cannot independently validate the hypothetical cool-roof intervention.
