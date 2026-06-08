<div align="center">

# ⚗️ ML-Driven Cyclic Voltammetry Prediction
## NiO/TiO₂ Nanocomposite Electrode Systems

**A publication-ready machine learning pipeline for electrochemical behavior prediction**  
Benchmarks **14 regression models** · Multi-scan-rate CV analysis · Research-grade visualizations

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3%2B-orange?style=flat-square&logo=scikit-learn&logoColor=white)](https://scikit-learn.org)
[![XGBoost](https://img.shields.io/badge/XGBoost-2.0%2B-red?style=flat-square)](https://xgboost.readthedocs.io)
[![LightGBM](https://img.shields.io/badge/LightGBM-4.0%2B-green?style=flat-square)](https://lightgbm.readthedocs.io)
[![CatBoost](https://img.shields.io/badge/CatBoost-1.2%2B-yellow?style=flat-square)](https://catboost.ai)
[![Colab](https://img.shields.io/badge/Colab-Ready-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com)
[![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Publication--Ready-brightgreen?style=flat-square)]()

[🔬 Overview](#-overview) · [🚀 Quick Start](#-quick-start) · [🤖 Models](#-models) · [📊 Outputs](#-outputs) · [📋 Input Format](#-input-format) · [📜 Citation](#-citation)

</div>

---

## 🔬 Overview

This repository contains the complete machine learning pipeline used to predict the **cyclic voltammetry (CV) electrochemical responses** of **NiO/TiO₂ nanocomposite electrodes** across multiple scan rates. The pipeline trains and benchmarks **14 regression algorithms** — from simple linear regression to advanced stacking ensembles — and automatically generates publication-quality figures and statistical tables.

> 🧪 **Material System:** NiO/TiO₂ Nanocomposites  
> 📈 **Task:** Current (A) prediction as a function of Potential (V) at multiple scan rates  
> 🏆 **Best Model:** Stacking Ensemble (RF + GBR + SVR → Linear Regression)

### Why this pipeline?

Electrochemical characterization produces large, multi-scan-rate datasets that are time-consuming to evaluate manually. This tool:

- ✅ Trains **14 models simultaneously** across all scan rates in one run
- ✅ Automatically applies **StandardScaler** for distance/kernel-based models (SVR, KNN, MLP)
- ✅ Generates **scatter, line, and boxplot** figures in smart adaptive layouts
- ✅ Produces a **Stacking Ensemble** from diverse base learners as a strong baseline
- ✅ Fully compatible with **Google Colab** — no local setup required

---

## 🚀 Quick Start

### ☁️ Option A — Google Colab *(recommended)*

1. Open the script in [Google Colab](https://colab.research.google.com/)
2. Upload your `.xlsx` CV data file when prompted
3. All figures are saved automatically per dataset

```python
# File upload is handled automatically via:
from google.colab import files
uploaded = files.upload()
```

### 💻 Option B — Local Installation

```bash
# 1. Clone the repository
git clone https://github.com/comsian-material-lab/ML-Driven-Cyclic-Voltammetry-Prediction-NiO-TiO2-Electrode-Systems.git
cd ML-Driven-Cyclic-Voltammetry-Prediction-NiO-TiO2-Electrode-Systems

# 2. Install dependencies
pip install -r requirements.txt

# 3. Add your .xlsx data to data/ folder
# 4. Run the pipeline
python src/main.py
```

---

## 🤖 Models

14 regression models are benchmarked on every scan rate. Models requiring normalized input are automatically scaled with `StandardScaler`.

| # | Model | Category | Scaling |
|---|-------|----------|---------|
| 1 | Random Forest | Ensemble (Bagging) | — |
| 2 | Gradient Boosting | Ensemble (Boosting) | — |
| 3 | Extra Trees | Ensemble (Bagging) | — |
| 4 | HistGradientBoosting | Ensemble (Boosting) | — |
| 5 | XGBoost | Ensemble (Boosting) | — |
| 6 | LightGBM | Ensemble (Boosting) | — |
| 7 | CatBoost | Ensemble (Boosting) | — |
| 8 | SVR | Kernel-based | ✅ |
| 9 | KNN (k=5) | Instance-based | ✅ |
| 10 | KNN (k=7) | Instance-based | ✅ |
| 11 | KNN (k=9) | Instance-based | ✅ |
| 12 | MLP Neural Network | Deep Learning | ✅ |
| 13 | Linear Regression | Linear | — |
| 14 | **Stacking Ensemble** | **Meta-learning** | — |

### 🏗️ Stacking Architecture

```
Base Learners                    Meta Learner
─────────────                    ────────────
Random Forest   ──┐
                  ├──▶  Linear Regression  ──▶  Final Prediction
Gradient Boost  ──┤
                  │
SVR  ─────────────┘
```

---

## 📊 Outputs

All outputs are saved automatically per dataset.

| File | Description |
|------|-------------|
| `scatter_combined.png` | Actual vs. Predicted — Stacking model, all scan rates |
| `combined_line.png` | MSE · RMSE · MAE · R² trends across scan rates for all 14 models |
| `combined_boxplots.png` | Metric distribution per model across scan rates |
| `Stacking_R2.png` | Cross-dataset R² comparison of Stacking Ensemble |
| `Stacking_RMSE.png` | Cross-dataset RMSE comparison |
| `Stacking_MAE.png` | Cross-dataset MAE comparison |
| `Stacking_MSE.png` | Cross-dataset MSE comparison |

---

## 📋 Input Format

Your `.xlsx` file must contain **column pairs** — one Potential column and one Current column — repeated for each scan rate:

```
┌──────────────────┬───────────┬──────────────────┬───────────┬─────┐
│ Potential_5mVs⁻¹ │  5 mVs⁻¹  │ Potential_10mVs⁻¹│  10mVs⁻¹  │ ... │
├──────────────────┼───────────┼──────────────────┼───────────┼─────┤
│     -0.800       │  1.23e-5  │     -0.800       │  1.45e-5  │ ... │
│     -0.750       │  2.10e-5  │     -0.750       │  2.33e-5  │ ... │
└──────────────────┴───────────┴──────────────────┴───────────┴─────┘
```

- Columns must come in **pairs**: `[Potential_col, Current_col]`
- The **current column name** is used as the scan rate label in all plots
- Missing values (`NaN`) are automatically dropped per column pair

---

## 📐 Evaluation Metrics

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| **MSE** | `mean((y − ŷ)²)` | Penalizes large errors heavily |
| **RMSE** | `√MSE` | Same unit as target — interpretable error magnitude |
| **MAE** | `mean(\|y − ŷ\|)` | Robust to outliers — average absolute deviation |
| **R²** | `1 − SSres/SStot` | Variance explained — 1.0 is perfect |

> For MSE, RMSE, MAE: **lower is better**. For R²: **higher is better** (max = 1.0)

---

## 📁 Project Structure

```
ML-Driven-Cyclic-Voltammetry-Prediction-NiO-TiO2-Electrode-Systems/
│
├── src/
│   └── main.py                  # Complete ML pipeline
│
├── data/                        # Place your .xlsx input files here
│
├── results/
│   └── figures/                 # Auto-generated output figures
│       ├── scatter_combined.png
│       ├── combined_line.png
│       ├── combined_boxplots.png
│       └── Stacking_*.png
│
├── requirements.txt             # Python dependencies
├── .gitignore
└── README.md
```

---

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `pandas` | ≥ 2.0.0 | Data loading and manipulation |
| `numpy` | ≥ 1.24.0 | Numerical operations |
| `matplotlib` | ≥ 3.7.0 | All visualizations |
| `scikit-learn` | ≥ 1.3.0 | Core ML models, metrics, preprocessing |
| `xgboost` | ≥ 2.0.0 | XGBoost regressor |
| `lightgbm` | ≥ 4.0.0 | LightGBM regressor |
| `catboost` | ≥ 1.2.0 | CatBoost regressor |
| `openpyxl` | ≥ 3.1.0 | Excel file support |

```bash
pip install -r requirements.txt
```

---

## 📜 Citation

If you use this code in your research, please cite:

```bibtex
@article{[citation_key],
  title   = {[Full paper title]},
  author  = {[Author 1] and [Author 2] and ...},
  journal = {[Journal Name]},
  year    = {[Year]},
  volume  = {[Volume]},
  pages   = {[Pages]},
  doi     = {[DOI]}
}
```

---

## 🔗 Related Repositories

| Repository | Material System |
|------------|----------------|
| [Electrochemical-Ml-Analysis](https://github.com/comsian-material-lab/Electrochemical-Ml-Analysis) | TiO₂–MnO₂ electrodes |
| [Pristine-and-Transition-Metal-Doped-TiO2-SiO2](https://github.com/comsian-material-lab/Pristine-and-Transition-Metal-Doped-TiO2-SiO2-Electrode-Systems) | TiO₂–SiO₂ electrode systems |
| [Data-Driven-CV-Prediction-MnO2-SiO2](https://github.com/comsian-material-lab/Data-Driven-Cyclic-Voltammetry-Prediction-Doped-Mno2-Sio2-Electrodes) | Doped MnO₂–SiO₂ electrodes |
| **This repo** | **NiO/TiO₂ nanocomposites** |

---

## 📝 License

This project is licensed under the **MIT License** — free to use, modify, and cite in academic work.

---

<div align="center">

Built for electrochemical research · Designed for reproducibility · Ready for publication  
**[comsian-material-lab](https://github.com/comsian-material-lab)** — Material Lab, COMSATS University

</div>
