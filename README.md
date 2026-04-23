# Anomaly Detection for Network Intrusion: UNSW-NB15 Benchmark

A comparative study of five machine learning methods for network intrusion detection on the [UNSW-NB15 dataset](https://research.unsw.edu.au/projects/unsw-nb15-dataset). Three unsupervised anomaly detectors (Isolation Forest, Local Outlier Factor, One-Class SVM) — trained exclusively on normal traffic with no labeled attack examples — are benchmarked against two supervised baselines (Random Forest, XGBoost) that train on labeled data under extreme class imbalance.

**Start here: [`main_notebook.ipynb`](main_notebook.ipynb)**

## Project Video
[![CSCE-676 Final Project: Anomaly Detection for Network Intrusion on UNSW-NB15](https://img.youtube.com/vi/1PPpK9C-YgE/0.jpg)](https://youtu.be/1PPpK9C-YgE)

---

## Research Question

> **How well do different anomaly detection methods perform on network intrusion detection with extreme class imbalance?**

Specifically: when models are trained exclusively on normal traffic (no labeled attacks), how close can they come to supervised methods that have full access to labeled attack examples?

---

## Results Summary

| Rank | Model | F1-Score | ROC-AUC | FPR |
|------|-------|----------|---------|-----|
| 1 | **XGBoost** | **0.917** | 0.983 | 0.035 |
| 2 | **Random Forest** | 0.890 | **0.985** | **0.003** |
| 3 | Isolation Forest | 0.785 | 0.706 | 0.625 |
| 4 | Local Outlier Factor | 0.809 | 0.574 | 0.998 |
| 5 | One-Class SVM | 0.721 | 0.528 | 0.743 |

Supervised methods dominate, but Isolation Forest is the strongest unsupervised option — robust to the dataset's temporal distribution shift where LOF and OCSVM collapse. Full analysis in [`main_notebook.ipynb`](main_notebook.ipynb).

---

## Repository Structure

```
Data-Mining/
├── main_notebook.ipynb       # Final deliverable — full pipeline & analysis
├── requirements.txt          # Pinned dependencies
├── checkpoints/
│   ├── Checkpoint1.ipynb     # Dataset selection, EDA on UNSW-NB15 
│   └── Checkpoint2.ipynb     # Research question formulation, method selection, experimental design
├── data/                     # Dataset files (see Data section below)
└── README.md
```

---

## Data

This project uses the **UNSW-NB15** dataset. Download the files from the [official UNSW page](https://research.unsw.edu.au/projects/unsw-nb15-dataset) and place them in the `data/` directory (excluded from this repo due to size):

```
data/
├── UNSW_NB15_training-set.csv
├── UNSW_NB15_testing-set.csv
├── UNSW-NB15_1.csv  (through _4.csv)
└── NUSW-NB15_features.csv
```

The notebook handles all preprocessing: missing value imputation, label encoding of categoricals, and standard scaling. The training set is filtered to normal-only traffic for the unsupervised models and subsampled to create extreme imbalance (~11% attacks) for the supervised models.

---

## How to Reproduce

### Option 1 — Google Colab (easiest)

1. Open [`main_notebook.ipynb`](main_notebook.ipynb) and click the **"Open in Colab"** badge, or go to [colab.research.google.com](https://colab.research.google.com), choose **GitHub**, and paste in this repo's URL.
2. Upload the required `data/` CSV files to Colab's file browser.
3. Run the notebook top-to-bottom — Colab has all major dependencies pre-installed. Install any missing ones with:
   ```python
   !pip install xgboost
   ```

### Option 2 — Local (Python 3.10)

```bash
git clone https://github.com/Tyler-Keener/Data-Mining.git
cd Data-Mining

python3 -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate

pip install -r requirements.txt
```

Then open `main_notebook.ipynb` in JupyterLab or VS Code and run top-to-bottom. Make sure the `data/` files are in place first.

---

## Key Dependencies

| Package | Version |
|---------|---------|
| Python | 3.10.18 |
| pandas | 2.3.3 |
| scikit-learn | 1.7.2 |
| xgboost | 3.2.0 |
| matplotlib | 3.10.8 |
| seaborn | 0.13.2 |

Full pinned list in [`requirements.txt`](requirements.txt).

---

## Contact

Tyler Keener · tdane23@tamu.edu · Texas A&M University

---

*This project was completed as part of the coursework for CSCE-676: Data Mining & Analysis at Texas A&M University, Spring 2026.*