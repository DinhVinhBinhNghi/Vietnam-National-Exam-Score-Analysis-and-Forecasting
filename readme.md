# Vietnam National Exam Score Analysis & Forecasting – A Time-Series ML/DL Project

> **Why this matters for quantitative research roles:** > This project demonstrates an end-to-end workflow on noisy, real-world time series data. It encompasses data engineering, statistical hypothesis testing, structural break detection, feature engineering, and multi-model forecasting with rigorous evaluation. The methodologies and analytical mindset applied here translate directly to financial time series analysis and systematic strategy research.

---

## 🎯 Objectives & Deliverables

### Objectives
* **ETL & Normalization:** Ingest multi-year, multi-schema exam score files (2023–2025) and produce a clean, analysis-ready dataset.
* **Exploratory Data Analysis (EDA):** Uncover trends, distributions, and cross-sectional patterns by subject, exam block, and province.
* **Statistical Testing:** Apply ANOVA and t-tests to validate group differences; compute effect sizes (Cohen’s d) to measure the strength of variations.
* **Structural Break Detection:** Identify regime shifts (e.g., the 2025 policy change) using advanced algorithms like PELT, CUSUM, and Bayesian Online approaches.
* **Forecasting 2026:** Build, compare, and tune ARIMA, tree-based models (RandomForest/XGBoost), and linear baselines; evaluate performance using MAE, RMSE, and MAPE.

### Key Deliverables
* `Clean_Data_2023-2025/`: Standardized CSVs categorized by subject, block, and province.
* **Analytical Notebooks:** `EDA.ipynb`, `ChangePoint.ipynb`, `Forecast2026.ipynb`.
* **Consolidated Report:** `Report/ReportProject.ipynb` (A single, runnable presentation summarizing the findings).

---

## 🏗️ Architecture

```text
PythonProject/  
├─ Raw_Data/                     # Raw 2023–2025 inputs  
├─ Clean_Data_2023-2025/         # Processed outputs  
├─ Module/                       # ETL + Stats  
│  ├─ Load_Data.py  
│  ├─ Processor_Data.py  
│  ├─ Analysis.py  
│  ├─ Export.py  
│  └─ ANOVA_ttest.py  
├─ Model/                        # Modeling layer  
│  ├─ ChangePoint/  
│  │  ├─ ChangePointPreparer.py  
│  │  ├─ ChangePointDetector.py  
│  │  └─ ChangePointAnalyzer.py  
│  └─ Forecast/  
│     ├─ ForecastSubjectModel.py  
│     └─ ForecastBlockModel.py  
├─ Notebook/                     # Exploratory/Development environment  
├─ Report/                       # Final presentation notebook  
├─ run_pipeline.py               # End-to-end ETL orchestrator  
└─ requirements.txt
```
---

## Quick Start

# 1. Clone and set up Python 3.10+ environment  
git clone <repo>  
cd PythonProject  
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate  
pip install -r requirements.txt  
  
# 2. Run the full ETL pipeline (Raw → Clean)  
python run_pipeline.py  
# → Clean data appears in Clean_Data_2023-2025/  
  
# 3. Launch notebooks  
jupyter lab  
# Open: Notebook/EDA.ipynb, ChangePoint.ipynb, Forecast2026.ipynb  
# For review: Report/ReportProject.ipynb
```
---

### 📊 **Core Analyses & Models**
# 1) Change Point Detection (Structural Break)
Algorithms: PELT (ruptures), CUSUM, Bayesian Online Change Point Detection (BOCPD).

Scope: Analyzed 9 subjects, 5 exam blocks, across 7 provinces.

Findings: Identified a consensus breakpoint in 2025 across 21/21 series (using PELT), with robust statistical validation via t-tests and Cohen’s d.

# 2) Forecasting 2026
Features Engineered: Lagged means, post-2025 structural break flags, and threshold rates (rate_ge_5, rate_ge_8).

Models Developed: ARIMA, Random Forest, XGBoost (global model), and Linear baselines for each subject.

Evaluation & Selection: Evaluated via MAE/RMSE/MAPE on a 2025 holdout set. The final model selection was optimized for the lowest MAE.

Block Share Forecasts: Implemented multi-output regression (Ridge + Softmax), with ARIMA ultimately selected as the top performer.

# 3) Statistical Rigor
Conducted comprehensive ANOVA across subjects/blocks followed by post-hoc t-tests.

Provided clear effect size interpretations (Weak/Medium/Strong).

Counterfactual Analysis: Compared linear trend "what-if" scenarios against actual 2025 data to quantify the impact of regime shifts.

