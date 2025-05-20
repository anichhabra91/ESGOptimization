
# ESG-Aware Portfolio Optimization using Regularization and Clustering

## Overview

This project develops a framework for constructing **sustainable and high-performing portfolios** using S&P 500 stocks (2019–2024), integrating ESG (Environmental, Social, Governance) metrics and carbon emissions into classical Sharpe ratio-maximizing optimization. The methodology combines **regularization**, **clustering**, and **environmental constraints** to achieve a balance between **financial returns and sustainability goals**.

## Key Objectives

- Maximize the Sharpe ratio of a portfolio
- Enforce minimum ESG thresholds and emission caps
- Improve portfolio robustness using variance regularization
- Filter investment universe using ESG-emission-aware clustering

## Data Sources

- **ESG & Carbon Emissions:** WRDS database (Sustainalytics, Refinitiv, MSCI)
- **Stock Prices:** Daily closing prices from Bloomberg
- **Timeframe:** 2019 to 2024 (monthly return series derived)

## Methodology

### 1. Baseline Optimization

Maximize Sharpe ratio subject to:
- Full investment constraint: \\( \\sum w_i = 1 \\)
- No short selling: \\( w_i \\geq 0 \\)

### 2. ESG-Constrained Optimization

Additional constraint:
- Minimum weighted ESG score: \\( \\sum w_i \\cdot ESG_i \\geq \\text{Threshold} \\)

### 3. Emission-Constrained Optimization

Emission limit constraint:
- \\( \\sum w_i \\cdot (\\text{Scope1}_i + \\text{Scope2}_i) \\leq \\text{Threshold} \\)

### 4. Regularization

Variance regularization using a constraint on portfolio volatility:
- \\( w^T \\Sigma w \\leq U \\)

### 5. Clustering-Based Filtering

K-Means clustering on:
- ESG + Sharpe Ratio
- ESG + Scope 3 Emissions

Used to reduce the universe before optimization.

## Optimization Portfolios

| Portfolio | Description |
|----------|-------------|
| P1 | Baseline (Sharpe-max only) |
| P2 | + Regularization |
| P3 | + ESG constraint |
| P4 | + Emission constraint |
| P5 | + Clustering on ESG + Sharpe |
| P6 | + Clustering on ESG + Scope 3 |

## Results

| Portfolio | Sharpe Ratio | ESG Score | Emissions | # Stocks | Turnover |
|----------|--------------|-----------|-----------|----------|----------|
| P1 | 1.086 | 42.52 | 103.61 | 14 | 0.255 |
| P2 | 1.181 | 45.73 | 115.83 | 17 | 0.218 |
| P3 | 1.162 | 46.86 | 117.86 | 17 | 0.220 |
| P4 | 1.303 | 45.22 | **90.00** | 17 | 0.207 |
| P5 | 0.573 | **60.42** | 90.00 | 7 | 0.125 |
| P6 | **1.456** | 45.04 | **90.00** | 16 | **0.163** |

**Observations:**

- Regularization improved Sharpe ratio and lowered turnover.
- ESG constraint increased the average ESG score as expected.
- Emission constraint lowered carbon footprint with minor performance gain.
- Clustering on ESG + Scope 3 achieved the **best trade-off**: highest Sharpe ratio, good ESG score, low emissions, and lower turnover.

## Conclusion

This study shows that **financial performance and sustainability can be jointly optimized**. Regularization and clustering techniques not only enhance robustness but also help reduce environmental impact without sacrificing returns. In particular, **clustering using ESG and Scope 3 emissions** emerged as the most effective method—balancing risk-adjusted returns, diversification, and carbon goals.

## References

- Ban et al. (2018), *Machine Learning and Portfolio Optimization*
- Le Guenedal & Roncalli (2022), *Portfolio Construction with Climate Risk*
- Park (2025), *Sharpe Ratio Optimization with Clustering*
- Wharton Research Data Services (WRDS)
