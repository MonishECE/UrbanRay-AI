# UrbanRay — AI-Assisted Urban Heat Screening

**Prototype research summary (not a verified Veritas submission).**

### Problem

Urban buildings absorb and exchange sunlight unevenly due to orientation, sky visibility and reflections from neighboring surfaces. Simplified solar calculations often ignore those reflections, while full simulation requires a geometric model. **UrbanRay asks whether a learned, physics-informed correction can predict missing reflected-sun absorption and screen hypothetical reflective-roof interventions across a documented urban block.**

### Approach

We used 88 documented NYC building footprints and heights, turned them into 2,082 simplified rooftop, wall and ground surface patches, and used an approximate multibounce physical radiation model to generate training labels. We compared two histogram-based gradient-boosting approaches: (1) directly predicting total absorbed shortwave radiation and (2) adding an AI-predicted **nonnegative reflection correction** to a simpler direct-plus-sky physical baseline. Training used earlier days; model selection used a separate validation day; the final test withheld both date and spatial blocks. We chose the model using validation only.

The app now runs three radiation options—full reference physics, the selected AI, and the direct-plus-sky baseline—within the same thermal simulator, with independent thermal histories. An offline dashboard explores AI/physics differences over time and compares dark roofs (assumed albedo 0.18) against reflective roofs (0.58), ranking building IDs by predicted reduction in daylight absorbed solar radiation.

### Results

On **20,976 held-out simulated surface-time records** (not field observations), the no-reflection baseline had a **7.90 W/m² MAE**, the direct AI had **4.14 W/m²**, and the validation-selected reflection-residual AI reached **3.63 W/m²** (**54.0% lower MAE than the baseline**). Physics versus AI rankings of the 88 building roof solar absorption changes on the demonstration day had **Spearman ρ≈0.999**. These measure agreement with the simulator, not measured effectiveness of cool roofs. A separate short synthetic-weather integration run confirmed the three codepaths work, but showed **AI inference was slower than sparse reference physics** at this scale; no acceleration claim is made.

### Limitations and next steps

Ground-truth roof-level temperatures and observed before/after interventions were not available. Roof materials and geometric simplifications were assumed, and the test data have correlated surfaces and hours. The existing Landsat analysis evaluates a thermal proxy separately, **not** the AI's measured temperature accuracy. Real-weather full thermal comparisons and independent seasonal/geographic tests are priorities. This is a **simulation-informed screening prototype**, not an operational retrofit recommendation.

### Sources / required credits

NYC Open Data building footprints; Open-Meteo historical gridded weather; USGS Landsat products (separate historical exploratory validation); scikit-learn; Plotly; OpenAI ChatGPT/GPT-6 coding and writing assistance. URLs and acknowledgments: `AI_UPGRADE_REPORT.md`. Team should verify author timelines and supply genuine personal contribution records. **Veritas 2026 forbids submitting an extension of a pre-event project.**
