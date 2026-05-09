# BRFSS 2015 Diabetes Screening

This repository contains a notebook-based analysis of diabetes risk using the 2015 Behavioral Risk Factor Surveillance System (BRFSS) survey data, with an external validation on BRFSS 2020.

## Abstract
Diabetes affects 537 million people globally; nearly half remain undiagnosed, with access barriers concentrated among low-income populations. Most machine learning screening models require clinical measurements unavailable to underserved groups, and the role of socioeconomic factors in risk remains poorly characterized.

## Introduction
BRFSS provides a large, questionnaire-based view of diabetes risk in the United States. This project evaluates whether non-clinical survey features can support screening models, and examines how socioeconomic factors (particularly income) relate to predictive performance and disparities.

## Methods
In this cross-sectional secondary analysis, I analyzed 249,049 BRFSS 2015 participants (binary diabetic outcome; pre-diabetics excluded by data curator) using four ML algorithms (logistic regression, decision tree, random forest, and XGBoost), a no-clinical-test reduced model, cross-algorithm permutation importance, targeted interaction terms, and LASSO-penalized interaction search. The no-clinical-test model underwent cross-year temporal replication (BRFSS 2020; n = 275,483).

## Results
On the de-duplicated primary dataset (n = 225,152; 23,897 duplicate records removed to eliminate fold contamination), the full model achieved ROC-AUC 0.814 (CV: 0.812) and the no-clinical-test model achieved 0.789 (sensitivity 75.0%, specificity 68.8%); cross-year replication yielded AUC 0.806. Income ranked consistently low across all algorithms using unified permutation importance (7th–21st); interaction modeling revealed income’s conditional associations (AUC 0.831–0.836). Diabetes prevalence declined 3.3-fold across income brackets; the lowest-income 32.7% of the sample accounted for 49.8% of cases. A fairness audit revealed a 37-percentage-point sensitivity range across income subgroups (equalized odds difference = 0.128); race and ethnicity data were unavailable and the income gradient should be interpreted cautiously.

## Conclusion
Questionnaire-based screening achieves meaningful discrimination without clinical measurements, but a fixed threshold produces severe disparate performance across income subgroups. Population-specific recalibration and prospective external validation are required before deployment.

## Repository contents
- `analysis.ipynb`: main analysis notebook.

## Data
- `diabetes_binary_health_indicators_BRFSS2015.csv`: curated BRFSS 2015 dataset used for the primary analysis (not included in the repo).
- `LLCP2020.XPT`: BRFSS 2020 raw data file used for external validation (update the path in the notebook if you place it elsewhere).

## Usage
1. Create a Python environment with typical data-science dependencies (pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn).
2. Place the data files in the repository root (or update the paths in `analysis.ipynb`).
3. Run `analysis.ipynb` in Jupyter or Colab.
