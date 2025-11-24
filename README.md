# Regression Analysis: Predicting Medical Insurance Charges

**Author:** Womenker Karto  
**Date:** 25-Nov-2025  

---

## Project Overview

This project demonstrates regression analysis on the **Medical Costs Dataset** to predict individual insurance charges based on demographic and health-related features. The dataset contains **1,338 records** with features such as age, sex, BMI, number of children, smoking status, and region.

The goal of this project is to:

- Explore and preprocess the dataset.
- Select features and engineer new ones.
- Train and evaluate regression models.
- Compare model performance and interpret findings.

---

## Dataset

The dataset is stored in the `data/` folder of this repository as `insurance.csv`.

**Features:**

| Feature   | Description |
|-----------|-------------|
| age       | Age of the individual |
| sex       | Gender (male/female) |
| bmi       | Body Mass Index |
| children  | Number of dependents |
| smoker    | Smoking status (yes/no) |
| region    | Residential area |
| charges   | Medical insurance charges (target variable) |

---

## How to Run the Notebook Locally

1. Clone the repository:
```bash
git clone https://github.com/wkarto/ml_regression_karto.git
cd ml_regression_karto
```
2. (Optional) Create a virtual environment:
```python
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```
3. Install required packages:
```python
pip install -r requirements.txt
```
4. Open and Run the Jupyter Notebook.

---

## Key Findings

    - Linear Regression with preprocessing (imputation + scaling) performed best with R² ≈ 0.785 on the test set.
    - Polynomial Regression (degree 3) did not improve performance, indicating the relationships are mostly linear.
    - Smoker status is the most influential feature on charges.
    - Outliers in the charges variable exist (~10%), and BMI extremes (~6.8%) were identified during exploratory data analysis.
    - Proper preprocessing, encoding categorical variables, and scaling numerical features were essential for robust model performance.

---

## Notebook & Peer Review Links

[Regression Notebook](./regression_karto.ipynb) 

[Peer Review Document](./peer_review.md)

---

## Future Work
    - Experiment with tree-based models (Random Forest, Gradient Boosting) for potential non-linear patterns.
    - Implement regularization techniques (Ridge, Lasso) to improve generalization.
    - Conduct feature importance analysis using SHAP values for better interpretability.



