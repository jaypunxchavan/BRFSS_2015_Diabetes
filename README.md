# BRFSS 2015 Diabetes Screening

This repository contains a notebook-based analysis of diabetes risk using the 2015 Behavioral Risk Factor Surveillance System (BRFSS) survey data, with an external validation on the BRFSS 2020 survey cycle.

## Manuscript Contents

### **Introduction.** Diabetes affects 537 million people globally; nearly half remain undiagnosed, with access barriers concentrated among low-income populations. Most machine learning screening models require clinical measurements unavailable to underserved groups, and the role of socioeconomic factors in risk remains poorly characterized.
### **Methods.** In this cross-sectional secondary analysis, I analyzed 249,049 BRFSS 2015 participants (binary diabetic outcome; pre-diabetics excluded by data curator) using four ML algorithms, a no-clinical-test reduced model, cross-algorithm permutation importance, targeted interaction terms, and LASSO-penalized interaction search. The no-clinical-test model underwent cross-year temporal replication (BRFSS 2020; n = 275,483).
### **Results**
On the de-duplicated primary dataset (n = 225,152; 23,897 duplicate records removed to eliminate fold contamination):
- Model performance: full model ROC-AUC 0.814 (CV: 0.812); no-clinical-test model AUC 0.789 (sensitivity 75.0%, specificity 68.8%); cross-year replication AUC 0.806.
- Income importance: income ranked 7th–21st across algorithms using unified permutation importance; interaction modeling showed conditional associations (AUC 0.831–0.836).
- Prevalence gradient: diabetes prevalence declined 3.3-fold across income brackets; the lowest-income 32.7% of the sample accounted for 49.8% of cases.
- Fairness audit: a 37-percentage-point sensitivity range across income subgroups (equalized odds difference = 0.128); race and ethnicity data were unavailable, so the income gradient should be interpreted cautiously. 
### **Conclusion.** Questionnaire-based screening achieves meaningful discrimination without clinical measurements, but a fixed threshold produces severe disparate performance across income subgroups. Population-specific recalibration and prospective external validation are required before deployment.

## Repository contents
- `analysis.ipynb`: main analysis notebook.

## Data
- `diabetes_binary_health_indicators_BRFSS2015.csv`: curated BRFSS 2015 dataset used for the primary analysis (located in repo). 
- `LLCP2020.XPT`: BRFSS 2020 raw data file used for external validation (located on the [CDC wesbite](https://www.cdc.gov/brfss/annual_data/2020/files/LLCP2020XPT.zip)).
## Usage
1. Create a Python environment with typical data-science dependencies (pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn).
2. Place the data files in the repository root (or update the paths in `analysis.ipynb`).
3. Run `analysis.ipynb` in a Jupyter environment.
