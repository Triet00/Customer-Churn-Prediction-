# Customer-Churn-Prediction-
## 1. Description
This project focuses on predicting player churn using gameplay data collected from January 2015 to May 2016, consisting of 163,929 rows and three columns: device, score, and time. The time variable indicates the Unix Epoch timestamp for each gameplay session.

## 2. Method
### 2.1 Preprocessing
Timestamps were standardized, missing device IDs (9 cases) removed, and exploratory analysis conducted (lifetimes, retention, scores, sessions). Insights guided OP/CP window selection and feature engineering.
### 2.2 Label Creation
OP/CP lengths were tested to balance misclassification risks, producing meaningful churn/no‑churn labels.
### 2.3 Feature Engineering
34 behavioral features (sessions, scores, engagement) were generated. Low‑variance filtering retained all; correlation pruning removed redundant pairs based on Random Forest importance.
### 2.4 Model Training
Severe class imbalance (93% churners for OP=7, CP=14) was mitigated with partial SMOTE (60/40 balance). Data was split into train/test and evaluated with 5‑fold CV. Models:
- Random Forest
- XGBoost 
- CatBoost
### 2.5 Hyperparameter Tuning
Randomized search optimized parameters, prioritizing ROC‑AUC and PR‑AUC.
### 2.6 Evaluation & SHAP
Performance metrics included accuracy, precision, recall, F1, ROC‑AUC, and PR‑AUC. SHAP analysis was applied to the best model.

## 3. Result
## 3.1 OP/CP Combination
Multiple OP/CP configurations (OP=1, CP=3 → OP=7, CP=14) were tested with stratified five‑fold CV. The (OP=7, CP=7) setup achieved the strongest metrics (ROC‑AUC=0.792, PR‑AUC=0.979, 95% churn capture) but produced extreme imbalance (95% churners). To avoid inflated performance, the (OP=7, CP=14) configuration was chosen as a more balanced alternative.
## 3.2 Model Comparison
Three ensemble models—Random Forest, XGBoost, and CatBoost—showed consistently strong performance after tuning. Overall, CatBoost delivered the best balance of accuracy and F1‑score, making it the selected model., with the following result:
- CatBoost: Acc=0.953, Prec=0.962, Rec=0.968, F1=0.965, ROC‑AUC=0.975, PR‑AUC=0.981
## 3.3 SHAP Analysis
SHAP analysis on the CatBoost model highlights temporal features as the strongest predictors.
- Top features: weekend_ratio, night_play_ratio, and active_days_ratio show the largest SHAP values and widest dispersions, indicating both strong impact and variability across users.
- Temporal indicators: avg_hour_of_day and peak_hour consistently push predictions upward with later activity, reinforcing the importance of daily timing.
- Recency & diversity: recency_days and hour_entropy provide stable contributions, capturing consistent behavioral patterns.
- Engagement & consistency: total_sessions, activity_days, and first_vs_avg_ratio exert moderate but reliable influence.


