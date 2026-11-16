## New decision task — 15 Nov 2026

The AI reflection-residual model selects high-reflection wall hotspots **against simulator reference labels** more effectively than a direct-exposure heuristic (top-20: 81.14% vs 11.46% of the simulator top-20 benchmark). On 3/5/10 held-out roof-portion selections it provides no decision improvement over no-reflection. A separate **previously completed physics-only** historical Landsat comparison remains exploratory and cannot be described as AI or measured cool-roof validation. A future time-matched three-path thermal evaluation tool was added but has no new observational scores. See `REAL_WORLD_UPGRADE_REPORT.md`.

---

## AI reflection-correction upgrade (15 November 2026)

- New AI model **learns the extra simulated shortwave absorption caused by reflections** rather than an observed roof temperature.
- Strict date + spatial-block held-out error: **3.635 W/m² MAE** vs **7.898 W/m²** no-reflection baseline. Both are relative to multibounce **simulated** labels.
- Building-level dashboard rankings are based on a June 23, 2025 physics-simulation day with assumed dark/reflective roof albedos. Rank correlation with simulator is not independent environmental validation.
- Three radiation codepaths now drive independent thermal states; two-hour synthetic-only smoke test verified execution. No real-weather thermal comparison of the new AI pathway is claimed in this package.
- Observed AI inference was **slower** than the sparse shortwave operator in the smoke benchmark. Do not claim accelerated simulation.
- Full methodology, audit and competition-rule caveats: `AI_UPGRADE_REPORT.md`.

---

# Scientific status — latest available evidence

**Observed-data comparison performed, but real-world roof-temperature accuracy remains unproven.**

- **Physics input:** 88 official NYC building records, simplified extruded meshes; material properties and some thermal boundary conditions are assumptions.
- **Simulator ML:** trained and tested against physically simulated shortwave absorption, not independently observed irradiance or roof temperature; `outputs/ml_holdout/` is the complete current simulator benchmark.
- **Independent satellite inputs:** the three latest Landsat 2025–2026 CSV exports at package root; 150 candidate scenes, 44 shortlisted scenes, 1,104 qualified resampled-grid-cell rows.
- **Exploratory comparison:** 10 acquisition scenes in `outputs/multidate_validation/scene_level_EXPLORATORY.csv`; five 2025 development, five 2026 subsequent evaluation scenes. 272 gridded (correlated) matches across scenes.
- **Held-out (2026) scene summary:** raw 3.526 °C MAE / 4.061 °C RMSE; post-calibration 2.341 °C MAE / 2.907 °C RMSE; all against a simplified modeled radiative emission proxy, not direct roof thermometer readings.
- **Uncertainty and representativeness:** native Landsat thermal support ~100 m; scene uncertainty about 3 K; simplified geometry/material/emissivity; time interpolation; no independent rooftop observations, no demonstrated cool-roof intervention outcome.
- **Reproducibility gap:** original ten-date archive includes summary tables only, not all weather inputs, per-date surfaces, QA matching and logs. Inputs can be fetched and runs reproduced online; compare hashes and dates before treating as reproduced.

**Suitable claim:** 'We compared simulated urban surface thermal proxies against independent Landsat satellite retrievals on ten acquisition dates and reported exploratory scene-level differences and their limitations.'

**Not suitable:** 'UrbanRay predicts real roof temperature to within 2.34 °C' or 'Reflective roofs are proven to cool real NYC roofs by the simulated amount.'

**Audit source:** `outputs/multidate_validation/audit/AUDIT_REPORT.md`. **Do not use synthetic fixtures in `tests/` as observed environmental data.**
