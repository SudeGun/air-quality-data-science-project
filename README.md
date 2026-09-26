# 🌍 Air Quality Data Science Project (India 2015 – 2020)

This repository contains an end-to-end data science project focused on environmental analytics using the `city_day.csv` dataset, which records daily air quality measurements across various Indian cities from 2015 to 2020. The project encompasses comprehensive data preprocessing, exploratory data analysis (EDA), unsupervised learning (clustering), and supervised classification workflows.

---

## 📌 Project Overview & Objectives
- **Theme:** Environmental Data Analytics
- **Dataset:** `city_day.csv` (29,531 rows, 16 features)
- **Primary Objectives:**
  1. Handle high missingness and anomalies across multiple air pollutant sensor readings through systematic imputation.
  2. Uncover the underlying geometric structure and groupings of pollution profiles using EDA and clustering techniques (K-Means, Agglomerative, DBSCAN).
  3. Predict the multi-class air quality category (`AQI_Bucket`) based on ambient pollutant concentrations using supervised classification models.

---

## 📂 Data Preprocessing & Cleaning Pipeline

1. **Missing Data Analysis:**
   - Identified significant missing rates across pollutant features, notably `Xylene` (~61.3%) and `PM10` (~37.7%).
   - Rows with missing target values (`AQI_Bucket`) were dropped to preserve ground truth integrity, leaving **24,850 clean instances**.
2. **Feature Engineering & Leakage Prevention:**
   - Extracted temporal features from the `Date` column: `Year`, `Month`, `Day`, and `DayOfWeek`.
   - Explicitly dropped the numeric `AQI` score from the feature matrix to eliminate target leakage into the classification models.
3. **Imputation:**
   - Numerical features were imputed using the **median** of each feature to remain robust against extreme outlier spikes.
   - Categorical columns were imputed using the **most frequent value (mode)**.
4. **Class Distribution & Imbalance:**
   - The dataset exhibits marked class imbalance across the 6 target categories (`Moderate`, `Satisfactory`, `Poor`, `Very Poor`, `Good`, `Severe`), with the vast majority concentrated in *Moderate* (8,829) and *Satisfactory* (8,224).

---

## 🔍 Exploratory Data Analysis (EDA) & Dimensionality Reduction

- **Correlation Matrix:** Strong positive collinearity was observed between traffic/combustion-related nitrogen oxides (`NO`, `NO2`, `NOx`) as well as between respirable particulate matters (`PM2.5`, `PM10`).
- **Principal Component Analysis (PCA):** Reducing the 17-dimensional standardized feature space down to 2 principal components revealed that the first two components account for only **33.97%** of the total variance, highlighting the complex, high-dimensional overlap among ambient pollution levels.

---

## 🤖 Unsupervised Learning: Clustering Analysis

Hyperparameter tuning across $k \in [2, 10]$ evaluated clustering performance via **Inertia**, **Distortion**, and **Silhouette Score**:
- The Elbow Method indicated a distinct rate-of-change transition at $k = 4$.
- Model performance metrics at $k = 4$:
  - **K-Means:** Silhouette Score = `0.3208`
  - **Agglomerative Hierarchical Clustering (Ward Linkage):** Silhouette Score = `0.1893`
- K-Means demonstrated substantially superior cluster separation and internal cohesion across dense pollution feature spaces.

---

## 🛠 Tech Stack & Libraries

- **Language:** Python 3.x
- **Data Manipulation & Analysis:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Machine Learning & Preprocessing:** `scikit-learn` (`StandardScaler`, `SimpleImputer`, `PCA`, `KMeans`, `AgglomerativeClustering`, `DBSCAN`, `classification_report`)
- **Distance Metrics:** `scipy.spatial.distance.cdist`
