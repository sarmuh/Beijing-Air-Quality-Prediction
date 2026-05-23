<div align="center">

# 🏙️ Beijing Air Quality: PM2.5 Prediction ML Pipeline

*An End-to-End Machine Learning Project for Predicting PM2.5 Air Pollution in Beijing.*

[![Status](https://img.shields.io/badge/Status-🚀_Active-brightgreen?style=for-the-badge)](https://github.com/)
[![Progress](https://img.shields.io/badge/Progress-80%25_Models_Trained-blue?style=for-the-badge)](https://github.com/)
[![Python](https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org)

</div>

---

## 📖 Table of Contents
1. [🎯 Project Overview](#-project-overview)
2. [📊 Dataset Information](#-dataset-information)
3. [🧠 Methodology & Pipeline](#-methodology--pipeline)
   - [Data Cleaning](#1️⃣-data-cleaning)
   - [Data Preprocessing & Feature Engineering](#2️⃣-data-preprocessing--feature-engineering)
   - [Modeling & Evaluation](#3️⃣-modeling--evaluation)
4. [📁 Project Structure](#-project-structure)
5. [🏆 Results](#-results)
6. [🚀 Next Steps](#-next-steps)

---

## 🎯 Project Overview

This project aims to build a robust **Machine Learning Pipeline** capable of predicting PM2.5 air pollution levels in Beijing, China. By leveraging multi-site meteorological and pollutant data, time-series feature engineering, and advanced regression models, the system helps forecast air quality to assist in environmental monitoring and public health planning.

---

## 📊 Dataset Information

The data comes from the UCI Machine Learning Repository's Beijing Multi-Site Air-Quality Data, collected from 12 air-quality monitoring sites.

| **Metric** | **Value** |
| :--- | :--- |
| 🗃️ **Raw Rows** | 420,768 (Across 12 stations) |
| 🧹 **Processed Rows** | 420,192 |
| 📍 **Location** | Beijing, China |
| 🎯 **Target Variable** | `PM2.5` (Concentration in µg/m³) |

### 🔑 Core Features
- `year`, `month`, `day`, `hour` - Temporal features.
- `TEMP`, `PRES`, `DEWP`, `RAIN`, `wd`, `WSPM` - Meteorological data (Temperature, Pressure, Dew Point, Rain, Wind Direction, Wind Speed).
- `station` - Categorical monitoring site data.
- Time-lagged and rolling mean features for various pollutants (PM2.5, PM10, SO2, NO2, CO, O3).

---

## 🧠 Methodology & Pipeline

The project development was divided into several focused stages inside Jupyter Notebooks:

### 1️⃣ Data Cleaning
> *Found in `01_cleaned.ipynb`*
- **Data Aggregation:** Merged 12 individual CSV files (one for each station) into a single unified dataset.
- **Initial Inspection:** Evaluated shape (420,768 rows) and foundational structure of the multi-site raw data.

### 2️⃣ Data Preprocessing & Feature Engineering
> *Found in `02_data_Preprocessing.ipynb`*
- **Handling Missing Values:** Cleaned data to prepare for time-series operations.
- **Feature Engineering (Time-Series):** 
  - ⏳ `shift24`: Created 24-hour lag features for pollutants and weather conditions (e.g., `PM2.5_shift24`, `TEMP_shift24`).
  - 🔄 `rolling_mean_24`: Calculated 24-hour rolling averages (e.g., `PM2.5_rolling_mean_24`).
  - 📉 `PM2.5_trend` & 🌡️ `Temp_Dewp_Diff`: Extracted trend signals and temperature-dew point differences.
- **Train-Test Split:** Created `train_data.csv` (403,200 rows) and `test_data.csv` (16,992 rows).
- **Transformation Pipeline:**
  - Standardized numeric features using `StandardScaler`.
  - Encoded categorical features (`station`, `wd`) using `OneHotEncoder`.
  - Combined transformations elegantly using Scikit-Learn's `ColumnTransformer`.

### 3️⃣ Modeling & Evaluation
> *Found in `03_training.ipynb`*
Fourteen different regression algorithms were trained and cross-validated, including:
1. **Linear Models** (Linear, Ridge, Lasso, ElasticNet, SGD)
2. **Tree-Based Models** (Decision Tree, Random Forest, Extra Trees)
3. **Boosting Models** (Hist Gradient Boosting, XGBoost, LightGBM, CatBoost)
4. **Others** (Linear SVR, KNN)

Each model was strictly evaluated utilizing `Root Mean Squared Error (RMSE)` and `R² Score`. 

---

## 📁 Project Structure

```text
Beijing-Air-Quality-Prediction/
├── 📄 README.md                          # You are here!
├── 📊 data/
│   ├── raw/
│   │   ├── PRSA_Data_Aotizhongxin...csv  # Initial raw dataset for stations
│   │   └── ...                           # (12 station files in total)
│   └── processed/
│       ├── train_data.csv                # Cleaned & split train dataset
│       └── test_data.csv                 # Cleaned & split test dataset
├── 🤖 models/                            # Directory for serialized models (Future use)
└── 📓 notebooks/
    ├── 01_cleaned.ipynb                  # Data Merging & Cleaning
    ├── 02_data_Preprocessing.ipynb       # Feature Engineering & Time-Series lags
    └── 03_training.ipynb                 # Model Training & Evaluation
```

---

## 🏆 Results

Upon evaluating the models on the hold-out test set, **Tree-based ensembles and Boosting models** significantly outperformed the baselines. The top performers were:

- 🏅 **Best Model:** `LightGBM Regression`
- 🎯 **Test RMSE Score:** **`71.235`**
- 📈 **R² Score:** **`0.596`**

*Honorable Mentions:*
- `Random Forest Regression`: RMSE 71.328 | R² 0.595
- `Hist Gradient Boosting`: RMSE 71.546 | R² 0.592

---

## 🚀 Next Steps

- [x] Merge and clean multi-site data.
- [x] Time-series feature engineering (24h lags, rolling means).
- [x] Train baseline and advanced regression models.
- [x] Model evaluation with RMSE and R² Score.
- [ ] 💾 **Export winning models** to `.jbl` / `.pkl` into the `models/` directory.
- [ ] 🔄 **Hyperparameter Tuning** for top models (LightGBM, Random Forest).
- [ ] 📈 **Advanced Error Analysis** (Evaluate Residuals, Feature Importance).
- [ ] 🌐 **Deployment** (Wrap the forecasting pipeline in a web service).

---
<div align="center">
  <i>Built with ❤️ utilizing</i><br><br>
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas" />
  <img src="https://img.shields.io/badge/Scikit_Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="Scikit-Learn" />
  <img src="https://img.shields.io/badge/LightGBM-ff6347?style=for-the-badge&logo=lightgbm&logoColor=white" alt="LightGBM" />
</div>