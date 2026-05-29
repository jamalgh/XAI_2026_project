# House Prices: R → Python Translation & Extension

**Reproducible Research — Final Project**  
University of Warsaw · 2025/26

---

## Authors

| Name | Role |
|------|------|
| [Name 1] | EDA, data loading, preprocessing |
| Otajon Yuldashev | LASSO & XGBoost translation, modelling |
| [Name 3] | Extension (Ridge, Elastic Net), conclusions, live demo |

---

## What This Project Does

This project translates an existing house price prediction analysis from R to Python.
The original analysis by Erik Bruin (Kaggle, 2018) uses LASSO regression and XGBoost
to predict sale prices of residential homes in Ames, Iowa using 79 features.

We reproduce the original results in Python, then extend the study by comparing three
regularization methods (LASSO, Ridge, Elastic Net) to test whether the original
conclusions hold across different model choices.

---

## Research Question

Can the results of Erik Bruin's R-based LASSO and XGBoost house price prediction
analysis be reproduced in Python, and does the choice of regularization method
(LASSO vs Ridge vs Elastic Net) alter the analytical conclusions?

---

## Original Source

Erik Bruin — *House Prices: LASSO, XGBoost and a detailed EDA*  
https://www.kaggle.com/code/erikbruin/house-prices-lasso-xgboost-and-a-detailed-eda  
Original language: R (`glmnet`, `xgboost`, `ggplot2`, `caret`)

---

## Key Results

| Model | CV RMSE | Type |
|-------|---------|------|
| LASSO (R original) | 0.1121 | Target |
| XGBoost (R original) | 0.1162 | Target |
| Elastic Net (Python) | 0.1254 | Extension |
| XGBoost (Python) | 0.1257 | Reproduction ✅ |
| LASSO (Python) | 0.1259 | Reproduction ✅ |
| Ridge (Python) | 0.1267 | Extension |

All four Python models cluster within a range of 0.0013 — confirming the original
conclusions are robust across regularization methods and model families.

---

## Data Source

Ames Housing Dataset — Kaggle House Prices Competition  
https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data

> ⚠️ Data must be downloaded manually due to Kaggle licensing restrictions.
> Download `train.csv` and `test.csv` and place them in `data/raw/`.

---

## Repository Structure

```
house-prices-r-to-python/
├── analysis.ipynb              ← main notebook — run this
├── data/
│   └── raw/                    ← place train.csv and test.csv here
├── outputs/
│   └── figures/                ← all plots saved here automatically
├── notebooks/
│   └── r_original/             ← Erik Bruin's original R notebook (reference)
├── environment.yml             ← conda environment (recommended)
├── requirements.txt            ← pip fallback
├── .gitignore
└── README.md
```

---

## Setup & How to Run

### Option A — Conda (recommended)

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_TEAM/house-prices-r-to-python.git
cd house-prices-r-to-python

# 2. Create and activate the environment
conda env create -f environment.yml
conda activate house-prices

# 3. Register the kernel so Jupyter/VS Code finds it
python -m ipykernel install --user --name house-prices --display-name "Python (house-prices)"

# 4. Download data from Kaggle and place in data/raw/
#    → train.csv and test.csv

# 5. Launch Jupyter
jupyter notebook
#    Open analysis.ipynb and select kernel "Python (house-prices)"
#    Then: Kernel → Restart Kernel and Run All Cells
```

### Option B — pip

```bash
git clone https://github.com/YOUR_TEAM/house-prices-r-to-python.git
cd house-prices-r-to-python
pip install -r requirements.txt
jupyter notebook
```

### Option C — No setup required (auto-install)

The notebook's first cell automatically installs any missing packages
using pip at runtime. Simply open `analysis.ipynb` and run all cells —
no manual installation needed.

---

## Expected Output

Running `analysis.ipynb` top to bottom (~3–5 minutes) produces:

- 6 plots saved to `outputs/figures/`
- Printed model comparison table with all CV RMSE scores
- Feature importance charts (LASSO coefficients, LASSO vs Ridge stability)
- Full conclusions in the final markdown cell

There are **no hardcoded results** — everything is regenerated from scratch.
Random seed is fixed at `np.random.seed(27)` to match the original R notebook.

---

## Software Environment

| Package | Version |
|---------|---------|
| Python | 3.11 |
| numpy | 1.26 |
| pandas | 2.2 |
| scikit-learn | 1.4 |
| xgboost | 2.0 |
| matplotlib | 3.8 |
| seaborn | 0.13 |
| scipy | 1.12 |

Full pinned versions in `environment.yml` and `requirements.txt`.

**Original R environment (for reference):**

| Package | Version |
|---------|---------|
| R | 4.3 |
| glmnet | 4.1 |
| xgboost | 1.7 |
| caret | 6.0 |
| ggplot2 | 3.4 |

---

## AI Support Disclosure

In accordance with course policy, this project used AI assistance as follows:

- **Tool:** Claude Sonnet 4.6 (Anthropic, 2026)
- **Scope:** Project scaffolding, README structure, code skeleton, and debugging
  assistance. All analytical decisions, model parameter choices, interpretations,
  and final results were produced and verified by the team. No AI-generated code
  was used without review and modification.

---

## Reproducibility Notes

- All file paths are relative — the notebook works from any machine
- The first cell auto-installs missing packages so no manual setup is required
- `data/raw/` is excluded from Git (see `.gitignore`) — download data from Kaggle
- `outputs/figures/` is included in Git so expected plots are visible without running
- Commit history shows individual contributions from each team member

---

## License

Academic use only. Original Kaggle analysis © Erik Bruin.  
Dataset © Dean De Cock / Kaggle.
