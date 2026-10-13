# DS-A2 — AI-Use and Independent-Verification Log

**Project:** Inference and Uncertainty in Sedimentary Phosphorite Geochemistry

**Source:** Ali et al. (2026), *Journal of Asian Earth Sciences*. DOI: 10.1016/j.jseaes.2025.106927.

**AI tool:** OpenAI ChatGPT

**Purpose:** To transparently document AI assistance, methodological decisions, computational checks, revised suggestions, and unresolved verification tasks.

## 1. Scope of AI Assistance

ChatGPT was used to support the development of a reproducible statistical investigation using published bulk-rock and in situ apatite geochemical observations.

The assistance included:

- Explaining sampling distributions, confidence intervals, bootstrap resampling, statistical power, and pseudoreplication.
- Suggesting Python code and analysis workflows for a Jupyter notebook in VS Code.
- Supporting data-cleaning decisions, computational troubleshooting, and reproducibility checks.
- Helping structure and draft the scientific method note, README, and verification documentation.

AI assistance was not treated as independent scientific evidence. Numerical results were obtained from executed analyses of the published dataset or clearly identified synthetic simulations.

## 2. Accepted AI-Assisted Methods

| Task | Accepted approach | Verification or qualification |
|---|---|---|
| Bulk-rock mean comparison | Welch unequal-variance confidence interval | Manually calculated limits agreed with SciPy |
| Sampling-distribution demonstration | Fixed-seed parametric Monte Carlo simulation | Simulated variability compared with the theoretical standard error |
| Study A uncertainty | Within-group nonparametric percentile bootstrap | Results compared with Welch interval; assumptions documented |
| Statistical power | Monte Carlo Welch tests across sample sizes, effects, and noise levels | Exported simulation results reloaded and checked |
| In situ apatite uncertainty | Parent-level summaries and layer-stratified cluster bootstrap | Parent-rock hierarchy examined; incomplete resamples recorded |
| Assumption counterexample | Paired synthetic parent-rock simulation | Empirical rejection rates and coverage estimated over 2,000 experiments |
| Reproducibility | Fixed random seeds and dependency recording | Restart-and-run-all check completed in VS Code |

## 3. Revised or Rejected Advice

**Treating analytical spots as independent geological replicates**

This was not adopted for the primary Study B uncertainty analysis. Multiple measurements within a parent rock can share geological characteristics; the analysis instead used parent-level summaries and parent-cluster resampling.

**Assuming pseudoreplication always increases false-positive rates**

This generalization was rejected. The synthetic counterexample found that treating balanced paired spots as independent produced overly conservative inference. The direction of error depends on the design and correlation structure.

**Interpreting the original bulk-rock contrast without lithological sensitivity**

This was revised by adding a phosphorite-only comparison. The estimated UPL–LPL difference declined from 210.30 ppm to 16.54 ppm, substantially changing its scientific interpretation.

**Treating 100 ppm as a validated geological threshold**

This was not accepted. The threshold is documented as a provisional meaningful-effect benchmark, not a geological or economic standard.

**Describing the research questions as prospectively preregistered**

This was rejected because the analysis was developed retrospectively from published observations. The notebook and method note describe the analysis as exploratory.

## 4. Independent Computational Verification

The following checks were performed or documented:

1. The original supplementary workbook was inspected, including six selected records covering the three stratigraphic layers across Tables S1 and S2.
2. Source-table stratigraphic group boundaries were examined.
3. The manually calculated Welch 95% confidence interval was compared with SciPy's unequal-variance t-test confidence interval, with numerical agreement.
4. Power-simulation results were exported as CSV files and reloaded for comparison.
5. Synthetic-counterexample results were exported and reloaded for comparison.
6. Random seeds and scientific Python package versions were recorded.
7. The notebook was executed from a restarted Jupyter kernel in VS Code without reported errors.
8. The scientific method note was exported to PDF, and equation rendering was visually checked.

These are implementation and documentation checks, not proof that all geological sampling assumptions hold.

## 5. Outstanding Verification and Limitations

- The six source records were selected for layer coverage rather than randomly.
- A separate direct programmatic comparison of those records against processed dataframes has not yet been documented.
- Parent-sample identifier interpretation has not been independently confirmed against original laboratory notebooks.
- Independent reproduction on a second computer has not been demonstrated.
- Historical failed runs have not been comprehensively archived.
- The Study B bootstrap percentile interval is based on 9,977 complete repetitions; 23 incomplete repetitions were excluded and reported.
- The analyses are observational and retrospective. Statistical intervals do not establish geological causation or sampling representativeness.

## 6. AI Responsibility Statement

ChatGPT contributed explanations, methodological suggestions, code-development support, troubleshooting, and draft documentation.

The researcher remained responsible for selecting the research questions, retaining the original data source, executing and inspecting the notebook, reviewing statistical interpretation, checking reported outputs, and deciding which suggestions were accepted or revised.

AI-generated suggestions were not considered verified solely because they produced executable code. The documented checks support reproducibility and internal consistency while leaving unresolved scientific assumptions explicit.

## 7. Reproducibility Records

The submission repository contains:

- `DS-A2_data_foundation.ipynb` — Executable analysis notebook.
- `Supplementary file.xlsx` — Original published supplementary dataset.
- `requirements.txt` and `requirements-lock.txt` — Dependency information.
- `results/` — Saved power and counterexample simulation results.
- `figures/` — Statistical visualizations.
- `docs/Method_Note.md` and `docs/Method_Note.pdf` — Scientific method and derivation note.
- `docs/AI_Verification_Log.md` — AI-use and verification record.

Repository version information and submission links will be recorded after GitHub publication.