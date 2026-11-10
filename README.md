# # DEKUT ML Masterclass — Phoenix Analytics

## Capstone Project — Group Three

This repository contains the complete codebase, analysis, and models for predicting wine quality based on physicochemical properties. This project was developed as a capstone for the **DEKUT ML Masterclass** by Phoenix Analytics.

### 👥 Group Members
- **John Mami** (Lead: EDA & Data Visualization)
- **Francis Njoroge** (Lead: Modeling & Metrics Evaluation)
- **Grace Chege** (Lead: Business Summary & Executive Synthesis)
- **Shadrack Muusya** (Lead: Presentation Slides & Q&A Prep)

---

## 📌 Problem Statement & Business Context

### Business Question
*"Can we predict whether a wine will be of high quality using its physicochemical properties?"*

### Target Variable
* **`quality`**: An integer score between `0` and `10` based on sensory evaluations conducted by wine-tasting panels.

### Real-world Business Value
For wineries, distributors, and retailers, predicting sensory quality objectively from laboratory measurements provides crucial quality control. It flags suboptimal batches *before* expensive expert tasting and distribution, helping managers optimize blending adjustments, standardize pricing tiers, and improve customer satisfaction.

---

## 📊 Dataset & Exploratory Data Analysis (EDA)
We combined the standard Red and White variants of the **UCI Wine Quality Dataset** (6,497 total samples) to form a robust, heterogeneous dataset.

### Key Findings from EDA:
1. **Data Completeness**: No missing values were found across all physicochemical attributes.
2. **Target Distribution**: Wine quality is moderately balanced but concentrated around the middle scores (`5` and `6`), with rare occurrences at the extremes (`3` and `9`).
3. **Core Correlations**: 
   * **Alcohol Content (`alcohol`)** exhibited the strongest positive correlation with wine quality.
   * **Volatile Acidity (`volatile acidity`)** showed a significant negative correlation, matching domain expectations (high volatile acidity produces an unpleasant vinegar-like taste).

---

## 🛠️ Machine Learning Pipeline

### Features Used
* **Primary Baseline Features**: `alcohol`, `volatile acidity`, `sulphates`, `wine_type_encoded` (Red = 0, White = 1).
* **Expanded Features (for improvements)**: All 11 chemical properties (including `fixed acidity`, `citric acid`, `residual sugar`, `chlorides`, `free sulfur dioxide`, `total sulfur dioxide`, `density`, and `pH`).

### Validation Strategy
* **Train/Test Split**: 80% train (5,197 samples) and 20% test (1,300 samples) with a fixed `random_state=42` to guarantee reproducibility.

---

## 📈 Experimental Results & Model Evaluation

We iteratively built and improved our models, using **Mean Absolute Error (MAE)** and **$R^2$ Score** as our regression metrics:

| Model | Features | MAE | $R^2$ Score | Status |
| :--- | :--- | :---: | :---: | :---: |
| **Always-Predict-Mean (Floor)** | None | 0.6691 | 0.0000 | Naive Baseline |
| **Linear Regression (Baseline)** | 4 Features | 0.5785 | 0.2546 | Beaten |
| **Decision Tree Regressor (v2)** | 7 Features | 0.5846 | 0.2361 | Overfitted |
| **Random Forest Regressor (Best)**| 12 Features | **0.5176** | **0.3916** | **Selected Best Model** |

### Key Takeaways:
* Our best model (**Random Forest Regressor**) reduced the prediction error by **22.6%** compared to the naive mean prediction model.
* On average, the model's predictions are within **0.517 quality points** of the actual sensory score.

---

## 💡 Key Business Recommendations

1. **Prioritize Key Chemical Profiles**: Focus quality assurance protocols primarily on regulating **alcohol levels** and limiting **volatile acidity**, as these chemical variables hold the highest predictive importance (~55.2% combined importance in the Random Forest model).
2. **Leverage Laboratory Synergy**: Standardize chemical testing labs to collect collective physicochemical features together. Individual variables on their own do not yield predictive accuracy, but when evaluated as a multi-dimensional system, they reduce assessment errors significantly.
3. **Deploy Random Forest for Prescreening**: Implement the Random Forest model as an automated, cost-effective screening step in the production pipeline. This allows batches to be pre-graded prior to expert human panels, reducing labor bottlenecks.
