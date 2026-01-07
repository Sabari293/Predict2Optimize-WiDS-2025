# Predict2Optimize — WiDS 2025  
**Predicting Market Dynamics for Data-Driven Portfolio Optimization**


# Week 1 — Financial Data & Feature Extraction
## Week 1: Financial Time Series Analysis
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
**Goals**
- Predict next-day returns using simple regression models.
- Establish performance baselines.

**Tasks**
- Use time-ordered train/test splits.  
- Implement:  
  - mean predictor (baseline)  
  - linear or ridge regression  
  - optional tree-based model (e.g., XGBoost)  
- Evaluate using standard regression metrics.

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
