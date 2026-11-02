# Credit Risk Modelling – Expected Loss Estimation

## Overview

This project explores the development of an Expected Loss (EL) model across a loan portfolio using three fundamental credit risk parameters:

- **Probability of Default (PD):** Likelihood of a borrower defaulting on their credit obligation.
- **Loss Given Default (LGD):** Proportion of exposure expected to be lost in the event of default, after accounting for recoveries.
- **Exposure at Default (EAD):** Expected outstanding exposure at the point of default.

Expected Loss is calculated using:

\[
EL = PD * LGD * EAD
\]

The project uses statistical modelling and machine learning techniques to estimate PD and LGD, integrates these estimates with portfolio exposure data, and derives expected losses at both individual loan and portfolio levels.

## Project Objectives

- Develop and compare alternative PD models using statistical and machine learning approaches.
- Estimate LGD using regression-based modelling techniques.
- Integrate PD, LGD and EAD to calculate Expected Loss.
- Evaluate model performance using appropriate classification and regression metrics.
- Examine available macroeconomic stress scenario data and its relationship with expected losses.

## Methodology

### 1. Data Exploration and Preparation

The analysis uses loan portfolio data and supporting datasets covering payment history, portfolio metrics and macroeconomic stress scenarios.

Key activities include:
- Data quality assessment and missing-value analysis.
- Examination of default rates and portfolio exposure distributions.
- Analysis of LGD and recovery rate characteristics for defaulted loans.
- Categorical feature encoding using one-hot encoding.
- Feature preparation using borrower, financial and loan-specific characteristics.

### 2. Probability of Default (PD) Modelling

PD models are developed using the following approaches:

| Model | Technique |
|---|---|
| Logistic Regression | Statistical classification benchmark |
| Random Forest | Ensemble classification |
| Gradient Boosting | Boosting-based classification |

**Model evaluation:**
- ROC-AUC: Measures discriminatory power.
- Gini Coefficient: Measures separation between defaulted and non-defaulted borrowers.
- Brier Score: Evaluates the accuracy of predicted default probabilities.

Gini is calculated as:

\[
Gini = (2 * AUC) - 1
\]

### 3. Loss Given Default (LGD) Modelling

LGD estimation is performed using defaulted loan observations, with the LGD variable serving as the target.

The following regression techniques are implemented:

| Model | Technique |
|---|---|
| Ordinary Least Squares (OLS) | Linear Regression |
| Ridge Regression | L2-regularised regression |
| Gradient Boosting Regressor | Ensemble regression |

Predicted LGD values are constrained to the interval [0, 1].

**Model evaluation:**
- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- R-squared

### 4. Exposure at Default (EAD) and Expected Loss

The project uses the existing EAD field from the loan portfolio dataset rather than developing an independent EAD prediction model.

For the portfolio-level calculation:

\[
EL_i = PD_i * LGD_i * EAD_i
\]

Where:

- \(PD_i\) = Estimated probability of default for loan \(i\).
- \(LGD_i\) = Estimated loss given default for loan \(i\).
- \(EAD_i\) = Exposure at default for loan \(i\).

Portfolio Expected Loss is calculated as:

\[
Portfolio\ EL = \sum_{i=1}^{N} EL_i
\]

The analysis also calculates the portfolio Expected Loss rate:

\[
EL\ Rate = \frac{Portfolio\ EL}{Total\ Portfolio\ EAD}
\]

### 5. Macroeconomic Stress Scenario Analysis

The notebook examines the available macroeconomic stress scenario dataset, including:

- Baseline and stressed PD.
- Baseline and stressed LGD.
- Sector-level EAD.
- Baseline and stressed Expected Loss.

This provides an overview of how stressed credit risk parameters are represented in portfolio loss analysis.

## Technology Stack

- **Programming:** Python
- **Data Manipulation:** Pandas, NumPy
- **Machine Learning:** Scikit-learn
- **Statistical Modelling:** Statsmodels, SciPy
- **Development Environment:** Jupyter Notebook

## Repository Structure

```text
Expected-Loss-Model/
│
├── Expected_Loss_Model.ipynb
│
├── loan_portfolio.csv
├── payment_history.csv
├── portfolio_metrics.csv
├── macro_stress_scenarios.csv
│
└── README.md
```

The CSV files represent the input datasets referenced by the notebook. Ensure they are available in the working directory before executing the relevant cells.

## How to Run

1. Clone the repository:

```bash
git clone <repository-url>
```

2. Navigate to the project directory:

```bash
cd Expected-Loss-Model
```

3. Install the required dependencies:

```bash
pip install pandas numpy scikit-learn scipy statsmodels jupyter
```

4. Launch Jupyter Notebook:

```bash
jupyter notebook
```

5. Open `Expected_Loss_Model.ipynb` and execute the cells sequentially.

## Scope and Limitations

- EAD is sourced from the existing loan portfolio dataset; an independent EAD/CCF model is not developed.
- The project focuses on PD and LGD estimation and their integration into Expected Loss calculations.
- The final portfolio predictions are generated using models fitted on the available dataset and should not be interpreted as independent out-of-sample estimates.
- Macroeconomic stress scenario data is examined, but a separate macroeconomic satellite model for stressed PD and LGD estimation is not developed.
- The implementation is an independent learning project and is not intended to represent a production-grade regulatory credit risk or IFRS 9 Expected Credit Loss framework.

## Disclaimer

This project is intended for educational and quantitative modelling purposes. The models and results should not be interpreted as production-ready credit risk estimates or regulatory model outputs.
