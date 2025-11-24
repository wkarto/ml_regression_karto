# Project Summary: Regression Model - Medical Insurance Charges Prediction

This document summarizes the key decisions, assumptions, and findings for the regression project predicting medical insurance charges using the Womenker Karto dataset. Complete each section clearly and professionally. 

---

## Problem Definition (Front Matter)

**Project Title:** Medical Insurance Charges Prediction  
**Author/Alias:** Karto  
**Brief description of the business or analytical problem:**  
The goal is to predict medical insurance charges (`charges`) for individuals based on demographic and health-related features such as age, BMI, smoking status, number of children, sex, and region. This helps insurers estimate costs and pricing strategies.

**What decision or action the model is intended to support:**  
Determine insurance premiums based on predicted medical costs.  

**Who would use this model:**  
Insurance companies and actuaries responsible for setting premiums and assessing risk.  

---

## 1. Target Variable

**Target variable name:** `charges`  
**Confirm the target is continuous and numeric:** Yes  
**Confirm no unexpected values, missing values, or outliers that distort the target:**  
- No missing values  
- Skewed distribution (skewness ≈ 1.52)  
- Outliers present in top 10% of charges  
**Why is this target meaningful for prediction:**  
Charges directly relate to insurance cost, a primary business metric. Accurate predictions allow fair and profitable premium setting.

---

## 2. Review Feature Variables

**List of available features:** `age`, `sex`, `bmi`, `children`, `smoker`, `region`  
**Are they numerical, categorical, or mixed:** Mixed (numerical: age, bmi, children; categorical: sex, smoker, region)  
**Are any features irrelevant or redundant:** None identified  
**Are any features ethically or legally restricted:** None  
**Could any features cause leakage:** No feature contains future outcome information  
**Example of possible leakage in this domain:** Using actual claims history from the future would leak information.  

---

## 3. Understand Relationships and Distributions

**Patterns or correlations observed:**  
- `charges` strongly influenced by `smoker` status  
- Moderate correlation with `age` (0.30) and `bmi` (0.20)  
- Minimal correlation with `children`  
- Categorical variables one-hot encoded  
- Outliers handled using IQR and extreme-value checks  

**Transformations applied:**  
- Standard scaling applied to numerical features  
- Categorical variables encoded (one-hot for `region` and `sex`; binary encoding for `smoker`)  
- No log-transform applied, model handled skewness adequately  

**Notable outliers:**  
- `charges` above 90th percentile (10% of data)  
- `bmi` extreme values ≥40 (6.8% of data)  

---

## 4. Select the Regression Model

**Baseline model chosen:** Linear Regression  
**Why it is appropriate:** Simple, interpretable, widely used for numeric prediction  
**Assumptions of the model:** Linearity, independence, homoscedasticity, normality of residuals  
**Are assumptions approximately met:**  
- Linearity partially met (scatterplots indicate mostly linear trend)  
- Residuals roughly homoscedastic  
- No severe multicollinearity (all correlations <0.3)

---

## 5. Evaluate Model Performance

**Metrics used:**  
- R², MAE, RMSE  
**How metrics were chosen:** Standard regression evaluation metrics, intuitive interpretation  
**Performance:**  
- Linear Regression: R² = 0.8668, MAE = 2733.21, RMSE = 4526.62  
- Pipeline 1 (scaled LR): R² = 0.7851, MAE = 4173.37, RMSE = 5750.75  
- Pipeline 2 (Polynomial deg 3): R² = 0.7823, MAE = 4173.65, RMSE = 5787.19  

**Performance interpretation:** Linear Regression captured majority of variance; scaling and polynomial transformation slightly reduced performance, indicating baseline LR is sufficient.  

**Error priorities:**  
- Overestimation slightly less critical than underestimation, as conservative premiums protect insurer profitability.

---

## 6. Improve the Model

**Alternate models/improvements tried:**  
- Pipeline with StandardScaler  
- Pipeline with Polynomial Features (deg 3)  
**Results:**  
- Scaling and polynomial features did not improve R²; slightly increased MAE and RMSE  
**Future improvements:**  
- Consider Ridge or Lasso regression for regularization  
- Explore interactions between BMI and smoker status  
- Test log-transformation on `charges` for normality  

---

## 7. Validate and Compare Models

**Comparison approach:** All models evaluated on same test set using R², MAE, RMSE  
**Best-performing model:** Linear Regression without scaling or polynomial features  
**Generalization confidence:** Test R² consistent with training metrics; model likely to generalize reasonably well.

---

## 8. Real-World Interpretation

**Feature influence insights:**  
- `Smoker` status has largest effect on charges  
- `Age` and `BMI` moderately increase expected charges  
- `Children` and `Region` less significant  
**Practical insights:**  
- Insurers can price policies based on age, BMI, and smoking status  
- Risk management strategies can target high-risk groups (smokers with high BMI)  
**Limitations:**  
- Model does not account for complex interactions beyond polynomial terms  
- Skewed charge distribution may require advanced models for extreme values  

---

## 9. Final Notes

**Key limitations:** Linear model cannot fully capture extreme outliers in charges  
**Future improvements:** Incorporate regularization, interaction terms, and advanced models (Random Forest, XGBoost)  
**Open questions:** Explore impact of lifestyle factors, regional health costs, or temporal changes in charges
