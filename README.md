# **Equity Portfolio Construction & Stock Selection with ML**

**Group 8:** Léo Linossier, Martin Belot, Vincent Gachon, Lucas Vachon

This project focuses on applying Machine Learning techniques to the finance sector, specifically for **Equity Portfolio Construction and Optimization**. By leveraging data-driven strategies, we aim to automate and enhance stock selection processes among a given list of stocks (e.g., S&P 500). Implementation of clustering algorithms (Unsupervised Learning) such as *K-Means* or *Hierarchical Clustering* to group stocks with similar characteristics. Usage of clusters to select uncorrelated assets for better portfolio diversification.

# **Context**

We are an asset manager that want to create a fund for a specific client that seeks a specific risk/return profile. Our fund contains equity, and we want to find the optmized approach to select to stocks we would like to include in our fund to match perfectly out$r client needs. 

| Parameter | Description |
| :--- | :--- |
| **Target Client** | **US Life Insurance Companies** |
| **Target Market** | USA |
| **Profile** | Long-term horizon, low risk tolerance, low need for immediate income. |
| **Key Constraints** | **High liquidity requirements** (to cover sudden claims/payouts). |

Strategy:

US Life Insurance companies struggle to fund their liabilities: very long-term obligations (10–30 years) often linked to annuity or life insurance contracts, combined with high liquidity needs for claims. Traditional solutions available to insurers (primarily bond portfolios or standardized mixed funds) have shown their limits: they either fail to generate sufficient yield to cover long-term liabilities or take on too much market or liquidity risk, potentially compromising liability stability.

Our project aims to address this specific need by offering a bespoke, simple, and transparent portfolio that combines liquidity, yield, and risk control. We propose constructing a liquid portfolio, predominantly fixed-income, supplemented by equities (20–25%) to enhance expected returns. This includes quantified yield and volatility targets (rather than guaranteed promises) and quarterly rebalancing to limit risk.

Detailed Proposed Strategy:

Risk Profile: Low target volatility, with a focus on capital preservation and liquidity management.

Asset Allocation:

Bonds (75–80%): Diversification between Government bonds (e.g., US Treasury 10Y) and Investment Grade Corporate bonds, with a duration focus adapted to liabilities.

Equities (20–25%): Selection of high-quality US stocks to improve expected yield while limiting volatility (e.g., JPM, 3M, PG).

Quantitative Objectives: Target yield, maximum volatility threshold, minimum liquidity level, with quarterly monitoring to adjust the portfolio according to market evolution.

This approach would allow the insurer to meet its liquidity and solvency requirements while optimizing the portfolio's long-term return, unlike the standardized solutions currently on the market.

### 1. K-Means Clustering (Benchmark)
* **Goal:** Establish a baseline grouping of assets.
* **Method:** Partition stocks into $k$ distinct clusters based on risk/return profiles.
* **Selection:** Identification of similar assets to avoid concentration.

### 2. Hierarchical Clustering
* **Goal:** Advanced structure analysis for risk diversification.
* **Method:** Build a dendrogram to visualize asset relationships and implement **Hierarchical Risk Parity (HRP)**.
* **Advantage:** Unlike K-means, this does not force a pre-defined number of clusters and captures nested correlations.

### 3. Genetic Algorithm (Optimization)
* **Goal:** Portfolio selection and weight optimization.
* **Method:** Use evolutionary principles (selection, crossover, mutation) to find the optimal combination of stocks.
* **Fitness Function:** Maximizing the Sharpe Ratio or minimizing Volatility under specific constraints.

Input: stock data $x$

Time window ?

Features: 

**1) Risk & Return Metrics**
- Return: Average daily stock returns
- Realized Volatility: Annualized standard deviation of daily returns
- Beta ($\beta$): Sensitivity to the broader market (e.g., S&P 500)
- Correlation: The pairwise correlation of daily returns is often used directly as a "distance" metric for clustering.
- Momentum: Returns over the past 3, 6 or 12 months

**2) Fundamental Ratios**
- These cluster stocks based on their company valuation and financial health.
- Valuation: P/E Ratio, P/B Ratio, EV/EBITDA.
- Profitability: ROE (Return on Equity), Net Margin.
- Leverage: Debt-to-Equity ratio.
- Size: Market Capitalization.

**3) Statistical Moments**
- Skewness: Measure of asymmetry in returns distribution.
- Kurtosis: Measure of "tail risk" (extreme events).
