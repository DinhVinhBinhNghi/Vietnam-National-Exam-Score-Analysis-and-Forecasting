# Vietnam National Exam Score Analysis & Forecasting
**Regime Detection · Time Series Modeling · ML-Based Forecasting**

An end-to-end time series analysis project covering data engineering, statistical validation, structural break detection, and multi-model forecasting on multi-year (2023–2025) real-world data.

> The workflow mirrors quantitative research pipelines:
> **Data → Validation → Regime Detection → Feature Engineering → Forecasting → Evaluation**

---

## 🎯 Objectives
* Standardize multi-year, multi-schema datasets into a clean analytical structure
* Detect and validate structural regime shifts
* Engineer regime-aware predictive features
* Compare statistical and ML forecasting models
* Perform holdout-based evaluation and model selection

## 📦 Deliverables
* **`Clean_Data_2023-2025/`**: Structured CSV exports by subject, block, and province
* **Research notebooks**: `EDA.ipynb`, `ChangePoint.ipynb`, `Forecast2026.ipynb`
* **Final consolidated report**: `Report/ReportProject.ipynb` (fully reproducible)

---

## 🏗 Architecture

```text
PythonProject/
├─ Raw_Data/                     # 2023–2025 raw inputs
├─ Clean_Data_2023-2025/         # standardized outputs
├─ Module/                       # ETL + statistical layer
│  ├─ Load_Data.py
│  ├─ Processor_Data.py
│  ├─ Analysis.py
│  ├─ Export.py
│  └─ ANOVA_ttest.py
├─ Model/                        # modeling layer
│  ├─ ChangePoint/
│  │  ├─ ChangePointPreparer.py
│  │  ├─ ChangePointDetector.py
│  │  └─ ChangePointAnalyzer.py
│  └─ Forecast/
│     ├─ ForecastSubjectModel.py
│     └─ ForecastBlockModel.py
├─ Notebook/
├─ Report/
├─ run_pipeline.py               # end-to-end ETL execution
└─ requirements.txt
```
---
## 📊 Structural Break Detection
**Goal**: Identify regime shifts in time series behavior.

**Algorithms Implemented:** PELT (ruptures), CUSUM, Bayesian Online Change Point Detection (BOCPD)

**Scope:**

9 subjects | 5 exam blocks | 7 provinces | 21 total time series

**Key Results:**

Consensus breakpoint detected in 2025 across 21/21 series (PELT).

Structural shift validated using: ANOVA, t-tests, and Cohen’s d effect sizes.

## 📈 Forecasting Framework (2026)
**Feature Engineering:** Lagged rolling means, Post-2025 regime flag, Threshold ratios (rate_ge_5, rate_ge_8), Cross-sectional block share features

**Models Compared:**

ARIMA

Linear regression baselines

RandomForest

XGBoost (global model)

**Evaluation:**

2025 holdout validation

MAE / RMSE / MAPE comparison

Model selection based on lowest MAE

**Block Share Forecasting:**

Multi-output Ridge regression + Softmax normalization

ARIMA selected as top-performing model in multiple series

## 🔬 Statistical Validation
- ANOVA across subjects and blocks

- Post-hoc t-tests

- Effect size interpretation (Weak / Medium / Strong)

- Counterfactual analysis: linear-trend baseline vs. actual 2025

---
## 🚀 Quick Start

**1. Set up Python 3.10+ environment**

git clone <repo>

cd PythonProject

python -m venv .venv

**Windows**

.venv\Scripts\activate

**macOS/Linux**

source .venv/bin/activate

pip install -r requirements.txt

**2. Run full ETL pipeline (Raw → Clean)**

python run_pipeline.py

_→ Outputs saved to Clean_Data_2023-2025/_

**3. Launch notebooks**

jupyter lab

Open: Notebook/EDA.ipynb, Notebook/ChangePoint.ipynb, Notebook/Forecast2026.ipynb

_For final review: Report/ReportProject.ipynb_
