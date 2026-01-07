# Predict2Optimize — WiDS 2025  
**Predicting Market Dynamics for Data-Driven Portfolio Optimization**

# Week 1: Financial Time Series Analysis
## Data Source
- **Yahoo Finance (`yfinance`)**
- Assets used:AAPL, MSFT, GOOG, AMZN, TSLANVDA (Tasks 5 & 6)
### Preprocessing
- Used *Adjusted Close* prices
- Missing values handled via forward-fill and back-fill
- Summary statistics obtained using `df.describe()`

---
## Task 1: Setup

**Key Steps**
- Download long-term and medium-term data
- Extract adjusted close prices
- Handle missing values
- Compute summary statistics

---

## Task 2: Basic Trends & Returns

**Objective**
Analyze short-term trends, returns, and volatility.

**Computed Metrics**
- Simple returns
- Log returns
- Rolling volatility

**Plots**
- Price vs 20-day moving average
- Log returns time series
- Rolling volatility comparison

**Observations**
- Prices closely track moving averages
- Volatility spikes during market stress (COVID)

---

## Task 3: Stationarity Analysis

**Objective**
To check whether returns are stationary.

**Methods**
- Rolling mean & rolling standard deviation (20, 60, 120 days)
- Augmented Dickey-Fuller (ADF) test

**Results**
- Mean of log returns is approximately stationary
- Variance is time-varying (volatility clustering)
- ADF test rejects non-stationarity (p < 0.05)

---

## Task 4: Volatility Regimes

**Objective**
Studied volatility clustering and crisis behavior.

**Volatility Estimators**
- 20-day rolling volatility
- EWMA volatility (λ = 0.94)

**Key Findings**
- EWMA is smoother and reacts faster to crashes
- EWMA is better suited for risk management
- Standardized returns have variance close to 1

---

## Task 5: Time Horizons and the “Normal” Illusion

**Objective**
Understand how return distributions change with time aggregation.

**Results**
| Horizon | Skewness | Kurtosis |
|------|---------|----------|
| Daily | -0.16 | 4.50 |
| Weekly | 0.08 | 1.30 |
| Monthly | 0.39 | 0.60 |

**Observations**
- Daily returns have fat tails
- Kurtosis decreases with longer horizons

---

## Task 6: Smart Investing
**Problem**
How many **RTX 4090 GPUs (~$1600 each)** could be bought today if $1000 was invested in **NVIDIA** on my birth date?

**Result**
- Equivalent to **~181 RTX 4090 GPUs**

---

# Week 2 — Baseline Models and Linear Predictors
##  Feature Construction

The following features were constructed:

- `r_t`
- `r_{t-1}`
- 20-day rolling mean of returns
- 20-day rolling volatility of returns
- 5-day momentum 

**Target**
- Next-day log return: `r_{t+1}`

---

##  Naive Baseline Models

Two naive baselines were implemented:

1. **Zero Predictor**
   - Predicts zero return every day
2. **Rolling Mean Predictor**
   - Predicts the past 20-day average return

These serve as **minimum performance benchmarks**.

---

##  Linear Model (OLS)

- Model: **Ordinary Least Squares (Linear Regression)**
- Inputs: engineered features
- Output: next-day return
  
---

##  Tree-Based Model (Random Forest)

- Model: Random Forest Regressor
- Parameters:
  - 100 trees
  - Max depth = 5
  - Minimum samples per leaf = 50

---

##  Walk-Forward (Time-Series) Evaluation

**Evaluation Strategy**
- Used `TimeSeriesSplit`
- We train past data and test it on future data

This avoids **data leakage**, which makes random train-test splits invalid for time-series forecasting.

---

##  Model Performance

### RMSE Comparison

| Model | RMSE |
|-----|-----|
| Zero Predictor | ~0.01831 |
| Rolling Mean | ~0.01855 |
| Linear | ~0.01815 |
| Random Forest | ~0.01819 |

- All models perform similarly
- Linear model slightly outperforms others

---

### Rolling RMSE Analysis

- Rolling RMSE (window = 100 days) plotted over time
- All models experience sharp error spikes during:
  - High-volatility
  - COVID crash (Feb–Mar 2020)

This highlights **model fragility during market stress**.

---

##  Volatility-Scaled Error

**Average Vol-Scaled Error**
- Zero: ~0.82
- Rolling Mean: ~0.84
- Linear: ~0.81
- Random Forest: ~0.81

---

##  Bonus: Toy Trading Strategy

- Go **long (+1)** if predicted return > 0
- Go **short (−1)** if predicted return < 0

**Results**
- Linear and Random Forest models generate higher cumulative returns
- Performance degrades during volatile periods

---

# References
- NumPy, Pandas, Matplotlib documentation  
- Scikit-Learn documentation  
- PyTorch quickstart  
- [`cvxpy` documentation](https://www.cvxpy.org/tutorial/index.html)  
- [PyPortfolioOpt documentation](https://pyportfolioopt.readthedocs.io/en/latest/)  
- [The Portfolio Optimization Book](https://portfoliooptimizationbook.com/) — Ch. 1–2–3 (Weeks 1–2), Ch. 6–8 (Weeks 4–5)  
- *Successful Algorithmic Trading* (general reference)  
- JAIR (2024):  
  **Decision-Focused Learning: Foundations, State of the Art, Benchmark and Future Opportunities**  
  — especially p. 40 for the Predict-to-Optimize portfolio framing.
