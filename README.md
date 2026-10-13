# DS-A2 | Inference and Uncertainty

## Project Overview

This repository contains a reproducible statistical investigation of rare earth element and yttrium (ΣREY) enrichment in sedimentary phosphorites, developed for the Data Science DS-A2 assignment.

The investigation uses published bulk-rock and in situ apatite geochemical observations from:

Ali et al. (2026), *Journal of Asian Earth Sciences*. DOI: 10.1016/j.jseaes.2025.106927.

The original supplementary Excel workbook is retained unchanged.

## Research Questions

**Study A — Bulk-Rock REY Enrichment**

How uncertain is the difference in mean bulk-rock ΣREY concentrations between the Upper Phosphorite Layer (UPL) and Lower Phosphorite Layer (LPL)?

The analysis includes sampling-distribution simulation, Welch confidence intervals, nonparametric bootstrap estimation, lithological sensitivity analysis, and Monte Carlo statistical power analysis.

**Study B — In Situ Apatite REY Enrichment**

How uncertain is the difference in mean ΣREY concentrations between pseudo-oolitic and pellet apatite when analytical measurements are nested within parent rock samples?

The analysis uses parent-level summaries, equal stratigraphic-layer weighting, and parent-cluster bootstrap resampling.

A synthetic counterexample examines the statistical consequences of ignoring dependence between analytical spots.

## Data

The file `Supplementary file.xlsx` contains the original published supplementary data.

- Supplementary Table S1: 29 bulk-rock observations.
- Supplementary Table S2: 103 in situ analytical spots from 26 parent rock samples.

Multiple analytical spots from the same parent rock are not treated as independent geological samples in the primary Study B uncertainty analysis.

No additional geological measurements were generated or represented as observed data. Synthetic datasets are used only for clearly identified statistical simulations.

## Project Files

```text
DS-A2_starter/
├── DS-A2_data_foundation.ipynb
├── Supplementary file.xlsx
├── README.md
├── requirements.txt
├── requirements-lock.txt
├── docs/
│   ├── Method_Note.md
│   ├── Method_Note.pdf
│   └── AI_Verification_Log.md
├── figures/
│   ├── Study_A_Confidence_Intervals.png
│   ├── Study_A_Power_Curves.png
│   └── Study_B_Counterexample_Comparison.png
└── results/
    ├── Study_A_Power_Results.csv
    └── Study_B_Counterexample_Results.csv
```

## Scientific Documentation and AI Verification

The completed scientific method note and AI-verification log are available in the `docs/` folder:

- `docs/Method_Note.md` — Editable statistical derivation and method note.
- `docs/Method_Note.pdf` — PDF version of the method note, including statistical equations and interpretation.
- `docs/AI_Verification_Log.md` — Record of AI-assisted tasks, accepted and rejected recommendations, independent computational checks, and outstanding verification limitations.

These documents complement the executable notebook and provide an audit trail for the statistical methods, reproducibility procedures, and responsible use of AI.

## Computational Environment

The analysis was executed using:

- Operating system: Windows 11
- Python: 3.13.9
- NumPy: 2.5.4
- pandas: 3.0.6
- SciPy: 1.18.1
- Matplotlib: 3.11.2
- openpyxl: 3.1.5

The exact installed dependency snapshot is recorded in `requirements-lock.txt`.

## Reproduction Instructions

1. Download or clone the repository.
2. Open the project folder in Visual Studio Code.
3. Install the Microsoft Python and Jupyter extensions if needed.
4. Create a Python virtual environment using Python 3.13.9.
5. Install the recorded dependencies.
6. Open `DS-A2_data_foundation.ipynb`.
7. Select the project Python environment as the notebook kernel.
8. Restart the kernel and execute all notebook cells from top to bottom.
9. Check the generated statistical figures, numerical results, and notebook validation outputs.

For Windows PowerShell, create the environment and install packages using:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-lock.txt
```

The notebook should be executed with its working directory set to the project root, where the supplementary Excel workbook is located.

## Reproducibility and Verification

Random seeds are specified in the statistical simulation cells.

The bulk-rock Welch confidence interval was independently checked against SciPy's implementation.

Power-simulation and synthetic-counterexample outputs were exported to CSV files and checked by reading them back into pandas.

The notebook has been executed from a restarted kernel without errors in the documented environment.

Reproducibility on a separate computer has not yet been independently tested.

## Statistical Limitations

The available geochemical data are observational and may not represent random geological samples.

Study A is sensitive to lithological composition, while Study B contains repeated analytical measurements nested within parent rocks.

Bootstrap and parametric confidence intervals depend on their respective assumptions. The synthetic counterexample represents a controlled hypothetical experiment and is not additional geological evidence.

The provisional 100 ppm meaningful-effect benchmark is a planning threshold rather than an independently established geological or economic cutoff.

## Data Provenance and Sharing

The original geochemical observations were published as supplementary material accompanying:

Ali et al. (2026), *Journal of Asian Earth Sciences*. DOI: https://doi.org/10.1016/j.jseaes.2025.106927.

The analysis uses the original supplementary Excel workbook, `Supplementary file.xlsx`, without modifying the source file.

**Public repository data availability:** The workbook is temporarily excluded from GitHub while its redistribution permissions are being clarified. No replacement or fabricated observational data are provided.

To reproduce the notebook, obtain the original supplementary workbook from the published article or its supplementary-material download page, place it in the repository root, and retain the exact filename `Supplementary file.xlsx`.

The statistical code, documentation, figures, and saved simulation results are included in the repository. The notebook requires the original workbook for complete execution.

Any subsequent changes to the dataset-sharing arrangements, code, analysis decisions, or outputs should be recorded through version control.


## AI Assistance

AI assistance was used to explain statistical concepts, suggest analysis methods and Python code, support troubleshooting, and draft methodological documentation.

Executed outputs, arithmetic checks, rejected or revised advice, and independent verification will be documented in the AI-use verification log before final submission.


