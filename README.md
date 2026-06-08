# Machine Learning Prediction of Electrochemical Behavior of NiO/TiO₂ Nanocomposites

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Publication--Ready-brightgreen)
![ML](https://img.shields.io/badge/ML-Scikit--Learn%20%7C%20XGBoost%20%7C%20LightGBM%20%7C%20CatBoost-orange)

> **Associated Publication:** *[Insert full paper title here]* — *[Journal Name]*, *[Year]*  
> **Authors:** *[Author 1], [Author 2], ...*  
> **DOI:** `[Insert DOI here]`

---

## Overview

This repository contains the complete machine learning pipeline used in our study on predicting the electrochemical (cyclic voltammetry) behavior of **NiO/TiO₂ nanocomposite** electrodes. Multiple scan rates are modeled simultaneously, and **14 regression algorithms** are benchmarked to identify the most accurate predictor of current response as a function of applied potential.

The pipeline is fully automated: given an Excel file of CV data (potential vs. current at multiple scan rates), it trains all models, evaluates performance, and generates publication-quality figures.

---

## Repository Structure

```
📦 ML_NiO_TiO2/
├── ML_NiO_TiO2.py          # Main pipeline script (Google Colab compatible)
├── requirements.txt         # Python dependencies
├── README.md                # This file
├── .gitignore               # Git ignore rules
└── sample_output/           # Example figures (optional)
    ├── scatter_combined.png
    ├── combined_line.png
    ├── combined_boxplots.png
    ├── Stacking_R2.png
    ├── Stacking_RMSE.png
    ├── Stacking_MAE.png
    └── Stacking_MSE.png
```

---

## Models Evaluated

| # | Model | Library |
|---|-------|---------|
| 1 | Random Forest | scikit-learn |
| 2 | Gradient Boosting | scikit-learn |
| 3 | Extra Trees | scikit-learn |
| 4 | Histogram Gradient Boosting | scikit-learn |
| 5 | Support Vector Regression (SVR) | scikit-learn |
| 6 | K-Nearest Neighbors (k=5) | scikit-learn |
| 7 | K-Nearest Neighbors (k=7) | scikit-learn |
| 8 | K-Nearest Neighbors (k=9) | scikit-learn |
| 9 | Multi-Layer Perceptron (MLP) | scikit-learn |
| 10 | Linear Regression | scikit-learn |
| 11 | XGBoost | xgboost |
| 12 | LightGBM | lightgbm |
| 13 | CatBoost | catboost |
| 14 | **Stacking Ensemble** (RF + GBR + SVR → LR) | scikit-learn |

---

## Evaluation Metrics

Each model is evaluated on a held-out test set (20%) using:

- **R²** — Coefficient of determination
- **MSE** — Mean Squared Error
- **RMSE** — Root Mean Squared Error
- **MAE** — Mean Absolute Error

---

## Input Data Format

The pipeline expects an `.xlsx` file where columns are arranged in pairs:

| Potential (V) @ 5 mVs⁻¹ | Current (A) @ 5 mVs⁻¹ | Potential (V) @ 10 mVs⁻¹ | Current (A) @ 10 mVs⁻¹ | ... |
|---|---|---|---|---|
| -0.5 | 0.0012 | -0.5 | 0.0015 | ... |
| ... | ... | ... | ... | ... |

- Each pair of columns represents one scan rate
- Column headers for current columns should include the scan rate label (e.g., `5 mVs-1`, `10 mVs-1`)
- Multiple Excel files can be processed in a single run

---

## Usage

### Option 1: Google Colab (Recommended)

1. Open [Google Colab](https://colab.research.google.com/)
2. Upload `ML_NiO_TiO2.py` and run it
3. When prompted, upload your `.xlsx` data file(s)
4. Output figures are saved automatically per file

```python
# The script handles upload automatically via:
from google.colab import files
uploaded = files.upload()
```

### Option 2: Local Environment

```bash
# 1. Clone this repository
git clone https://github.com/[your-username]/ML_NiO_TiO2.git
cd ML_NiO_TiO2

# 2. Install dependencies
pip install -r requirements.txt

# 3. Modify the file loading section for local use:
#    Replace the Colab upload block with:
#    file_names = ["your_data.xlsx"]

# 4. Run
python ML_NiO_TiO2.py
```

---

## Output Figures

The pipeline automatically generates the following figures for each input file:

| Figure | Description |
|--------|-------------|
| `scatter_combined.png` | Actual vs. predicted current scatter plots for each scan rate (Stacking model) |
| `combined_line.png` | MSE, RMSE, MAE, and R² trends across scan rates for all 14 models |
| `combined_boxplots.png` | Distribution of all metrics across scan rates per model |
| `Stacking_R2/RMSE/MAE/MSE.png` | Cross-file comparison of Stacking Ensemble performance |

---

## Requirements

See [`requirements.txt`](requirements.txt) for the full list. Key dependencies:

```
scikit-learn
xgboost
lightgbm
catboost
pandas
numpy
matplotlib
openpyxl
```

---

## Citation

If you use this code in your research, please cite our paper:

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

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## Contact

For questions or collaborations, please contact:  
📧 **Safi Ullah Majid** — `[Safeullahmajid@gmail.com]`  
🔗 [ORCID](https://orcid.org/0009-0002-0942-5112]) | 
