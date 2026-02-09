Parkinson’s Disease Progression Prediction (Temporal Modeling)
📌 Project Overview

This project builds a temporal machine learning model to predict future changes in motor symptoms of Parkinson’s disease patients using the UCI Parkinson’s Telemonitoring dataset.

Instead of predicting absolute severity scores, the model focuses on predicting the change in motor UPDRS (ΔUPDRS) between visits, which better reflects disease progression dynamics and reduces patient-specific bias.

The final solution is clinically interpretable, leakage-safe, and deployment-ready.

🎯 Objectives

Model short-term disease progression using temporal features

Prevent data leakage via GroupKFold (patient-level splits)

Identify which patients are predictable vs unstable

Build a deployable regression model for real-world use

📊 Dataset

Source: UCI Parkinson’s Telemonitoring Dataset (via Kaggle)

Subjects: 42 patients

Observations: Longitudinal clinical visits

Target Variable:

updrs_delta = change in motor UPDRS from previous visit

🧠 Key Modeling Insight

Parkinson’s progression is not uniformly predictable.

Model errors are driven more by patient-specific disease volatility than by missing features. Stable patients show highly predictable progression, while unstable patients exhibit intrinsic unpredictability.

This insight is a core contribution of the project.

🔬 Feature Engineering
Static Features

Jitter

Shimmer

Harmonics-to-noise ratio (HNR)

RPDE

PPE

Sex

Temporal Features

updrs_lag1 – previous visit change

updrs_lag2 – two visits back

updrs_roll3 – rolling mean (3 visits)

baseline_updrs – first observed severity (used in analysis)

updrs_delta – modeling target

All temporal features are causal and leakage-free.

🤖 Models Evaluated
Model	Purpose
Dummy Regressor	Baseline comparison
Linear Regression	Interpretability
Ridge Regression	Final production model
Random Forest	Non-linear baseline
Final Model

✅ Ridge Regression with temporal features

Why Ridge?

Stable under collinearity

Interpretable coefficients

Strong generalization

Clinically defensible behavior

📈 Performance Summary

Cross-validated R²: ~0.90+

Test RMSE: Low and stable

Direction accuracy: High (captures trend correctly)

Importantly:

High error patients are clinically unstable, not modeling failures.

🧪 Error Analysis

Patients were stratified by:

Error magnitude

Baseline severity

Visit count

Progression volatility

Key finding:

Low-variance patients → accurate predictions

High-variance patients → unpredictable by nature

This reinforces the importance of volatility-aware clinical interpretation.

🔮 Prediction Contract

Input: Patient’s recent UPDRS history + voice features
Output: Predicted change in motor UPDRS at next visit

Interpretation:

Positive → worsening symptoms

Negative → improvement

Near zero → stability

⚠️ Limitations

Medication changes not available

No wearable or lifestyle data

Model does not capture sudden clinical events

These are data limitations, not modeling flaws.

🧭 Future Work

Volatility-aware risk classification

Bayesian uncertainty estimation

Patient-specific adaptive models

Integration into clinical dashboards

🏁 Conclusion

This project demonstrates that:

Temporal modeling significantly improves Parkinson’s progression prediction

Patient-specific volatility defines the upper bound of predictability

Interpretable ML can support, not replace, clinical judgment