# 💧 Water Quality Index Analysis & Prediction

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-Enabled-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)

![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=flat-square&logo=kaggle&logoColor=white)
![Best Model](https://img.shields.io/badge/Best%20Model-Linear%20Regression-blueviolet?style=flat-square)
![R2 Score](https://img.shields.io/badge/Best%20R²-0.9916-blue?style=flat-square)
![Models](https://img.shields.io/badge/Models%20Compared-6-orange?style=flat-square)

</div>

---

## 📌 Overview

This project develops a **machine learning regression pipeline** to predict the **Water Quality Index (WQI)** using physicochemical and microbiological water chemistry measurements. WQI is a composite score that summarizes the overall health of a water body into a single interpretable number — making its accurate prediction vital for environmental monitoring, public health, and resource management.

Six regression algorithms are benchmarked end-to-end, from raw data to final model selection, with **Linear Regression** emerging as the clear winner at an R² score of **0.9916**.

> **Goal:** Predict WQI from water chemistry features to enable automated, scalable water quality monitoring without manual index computation.

---

## 📊 Dataset

| Property | Detail |
|---|---|
| **Source** | [Kaggle — Water Quality Index (WQI)](https://www.kaggle.com/datasets/seyedarmanhossaini/water-quality-index-wqi) |
| **File** | `Results_MADE.csv` |
| **Records** | 295 rows |
| **Features** | 9 physicochemical & microbiological parameters |
| **Target** | Water Quality Index (WQI) — continuous numeric |
| **Missing Values** | None |
| **Duplicates** | None |

### Feature Columns

| Feature | Type | Description |
|---|---|---|
| Temperature | Float | Water temperature (°C) |
| Dissolved Oxygen | Float | DO concentration (mg/L) |
| pH | Float | Acidity/alkalinity level |
| Bio-Chemical Oxygen Demand | Float | BOD in mg/L |
| Faecal Streptococci | Float | MPN / 100 mL |
| Nitrate | Float | Nitrate in mg/L |
| Faecal Coliform | Float | MPN / 100 mL |
| Total Coliform | Float | MPN / 100 mL |
| Conductivity | Float | Electrical conductivity (mho/cm) |
| **WQI** | Float | **Target variable** |

> 🔑 **Key insight:** Conductivity is nearly 100% correlated with WQI, making it the dominant predictor in the dataset.

---

## 🔬 Project Pipeline

```
Raw Dataset (Kaggle — 295 rows, 10 columns)
        │
        ▼
Data Preparation
  ├── Null value check → None found
  ├── Duplicate check → None found
  └── Data type verification → All float64
        │
        ▼
Exploratory Data Analysis
  ├── WQI distribution (right-skewed histogram)
  ├── Feature distributions with normal curve overlays
  ├── Box plots → outliers detected
  ├── Pairplot (KDE diagonal)
  ├── Correlation heatmap
  └── Bar chart: top features correlated with WQI
        │
        ▼
Data Transformation
  ├── Outlier capping via IQR method (replace with median)
  ├── Post-capping distribution verification
  ├── Feature / target split (X, y)
  ├── Train-test split → 80% / 20% (236 train / 59 test)
  └── Standard scaling (StandardScaler)
        │
        ▼
Model Training & Evaluation (6 models)
  ├── Linear Regression
  ├── Decision Tree Regressor
  ├── Random Forest Regressor
  ├── Support Vector Regressor (SVR)
  ├── K-Nearest Neighbors Regressor
  └── Gradient Boosting Regressor
        │
        ▼
Model Comparison & Selection
  └── Best Model: Linear Regression (R² = 0.9916)
```

---

## 🤖 Models & Results

### Performance Summary

| Rank | Model | MSE | R² Score |
|---|---|---|---|
| 🥇 1 | **Linear Regression** | **4.7834** | **0.9916** |
| 🥈 2 | Random Forest Regressor | 13.1203 | 0.9770 |
| 🥉 3 | Gradient Boosting Regressor | 14.3288 | 0.9748 |
| 4 | Decision Tree Regressor | 66.0134 | 0.8840 |
| 5 | K-Nearest Neighbors Regressor | 123.5709 | 0.7829 |
| 6 | Support Vector Regressor | 259.2709 | 0.5445 |

> ✅ **Best Model: Linear Regression** — R² = **0.9916**, MSE = **4.78**

### Why Linear Regression Wins

The near-perfect R² of Linear Regression is explained by the near-perfect linear relationship between **Conductivity** and WQI. Since WQI is itself computed as a weighted linear combination of physicochemical parameters, a linear model captures this structure directly — outperforming all tree-based and kernel-based alternatives on this dataset.

---

## 🔑 Key Findings

- **No missing or duplicate values** — the dataset was clean and required no imputation
- **Right-skewed WQI distribution** — most observations cluster at lower WQI values, with a long tail
- **Conductivity dominates** — nearly 100% correlated with WQI, making it the single most predictive feature
- **Outliers present** — IQR-based median capping was applied to all 10 columns before modelling
- **Linear structure** — WQI is linearly derivable from the feature set, which explains the dominance of Linear Regression
- **SVR underperforms** — with an R² of only 0.5445, kernel-based methods struggle with the scale disparity across features even after standardization
- **Feature scaling essential** — StandardScaler was required due to the extreme range differences between features (e.g., Conductivity vs pH)

---

## 🛠️ Tech Stack

```python
pandas         # Data loading and manipulation
numpy          # Numerical operations
matplotlib     # Plotting (histograms, bar charts, box plots)
seaborn        # Statistical visualizations (heatmap, pairplot, barplot)
missingno      # Missing value visualization
scikit-learn   # All ML models, preprocessing, train-test split, metrics
scipy          # Normal distribution overlay on histograms
kagglehub      # Dataset download from Kaggle
```

**Environment:** Google Colab

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/MuhammadUsman-Khan/Water-Quality-Index-Analysis-and-Prediction.git
cd Water-Quality-Index-Analysis-and-Prediction
```

### 2. Install Dependencies
```bash
pip install pandas numpy matplotlib seaborn missingno scikit-learn scipy kagglehub
```

### 3. Run the Notebook
Open `Water_Quality_Index_Analysis_&_Regression.ipynb` in Jupyter or Google Colab.

The dataset is automatically downloaded from Kaggle:
```python
import kagglehub
path = kagglehub.dataset_download("seyedarmanhossaini/water-quality-index-wqi")
```

> ⚠️ A Kaggle account and configured API credentials are required for `kagglehub` to work.

---

## 📁 Repository Structure

```
Water-Quality-Index-Analysis-and-Prediction/
│
├── Water_Quality_Index_Analysis_&_Regression.ipynb   # Main notebook
└── README.md                                          # Project documentation
```

---

## 🔮 Future Improvements

- [ ] Incorporate additional water quality datasets to improve generalizability
- [ ] Apply log transformation to right-skewed features for improved model stability
- [ ] Perform hyperparameter tuning (GridSearchCV) on tree-based models
- [ ] Add SHAP values for model interpretability and feature attribution
- [ ] Build a WQI classification layer on top of regression (Excellent / Good / Poor / Very Poor)
- [ ] Deploy as a REST API or Streamlit web app for real-time WQI prediction

---


## 🙋‍♂️ Author

**Muhammad Usman Khan**

[![GitHub](https://img.shields.io/badge/GitHub-MuhammadUsman--Khan-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/MuhammadUsman-Khan)

---

<div align="center">
  <i>If you found this project useful, consider giving it a ⭐ — it helps others discover it!</i>
</div>
