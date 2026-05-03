# Caravan Insurance Purchase Prediction
## MA679 Final Project | Spring 2026 | Madeleine Livaudais

---

## Project Overview
Analysis of the Caravan (TIC Benchmark) dataset to predict caravan insurance 
purchase using propensity score matching and 12 classification methods. 
Original dataset contains 5,822 observations, 85 ordinal predictors, and a 
heavily imbalanced binary response variable (6% purchasers).

---

## Data
- **Source:** ISLR2 package in R (`data(Caravan)`)
- **Original:** 5,822 observations, 85 predictors, 1 binary response (Purchase)
- **Matched:** 696 observations (348 purchasers, 348 non-purchasers)
- **Predictors:** All ordinal — sociodemographic (zip-code derived) and 
  insurance product ownership variables
- **Response:** Purchase (0 = No, 1 = Yes)
- **Data Dictionary:** CoIL Challenge 2000, Sentient Machine Research 
URL: (https://liacs.leidenuniv.nl/~puttenpwhvander/library/cc2000/data.html)

---

## Methodology

### 1. Pre-processing
- Propensity score matching (PSM) via `MatchIt` to address 94/6 class imbalance
- 1:1 nearest neighbor matching on all 85 predictors
- Balance verified via Love plot (standardized mean differences)

### 2. Unsupervised Learning (Ch. 12)
- Gower distance matrix via `daisy()` — appropriate for ordinal data
- Hierarchical clustering with Ward's linkage
- k=2 selected via scree plot

### 3. Supervised Classification Methods
All methods evaluated on same 80/20 train/test split via AUC (ROC curve)
10-fold cross-validation used for hyperparameter tuning throughout

| Method | Chapter | AUC |
|--------|---------|-----|
| Ridge Regression | Ch. 6 | 0.601 |
| Random Forest | Ch. 8 | 0.585 |
| Bagging | Ch. 8 | 0.583 |
| Radial SVM | Ch. 9 | 0.576 |
| Lasso Regression | Ch. 6 | 0.571 |
| Linear SVM | Ch. 9 | 0.571 |
| Splines | Ch. 7 | 0.568 |
| Logistic Regression | Ch. 4 | 0.564 |
| Forward Stepwise | Ch. 6 | 0.555 |
| LDA | Ch. 4 | 0.555 |
| Single Tree | Ch. 8 | 0.508 |
| Boosting | Ch. 8 | 0.450 |

---

## Key Findings
- Ridge regression performed best (AUC = 0.601) — regularization handled 
  severe multicollinearity among zip-code derived predictors
- All methods showed weak predictive signal (AUC 0.55-0.60), consistent with 
  the challenging nature of insurance purchase prediction
- Consistent predictor subset identified across methods: PGEZONG (family 
  accident insurance), PPERSAUT (car policies), MOPLMIDD (education level), 
  MGODGE (no religion), MINK7512 (income 75-122k)
- QDA failed due to rank deficiency — too many parameters per class
- Boosting failed to find stable sequential signal across all tuning attempts
- Two customer segments identified via clustering but with identical purchase 
  rates (~50%), suggesting customer profiles exist but do not predict purchase

---

## Methods Not Fully Applied & Reasons
- **QDA:** Rank deficient — 77 predictors exceeds 348 observations per class
- **Splines:** Applied to MOPLMIDD only — most predictors too sparse/zero-inflated
- **Best Subset Selection:** Computationally infeasible with 85 predictors (2^85 models)
- **Backward Stepwise:** Avoided due to full model instability (extreme coefficients, NAs)

---
