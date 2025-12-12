# **Data Project (Group 8)**

**Group composition**

Léo Linossier

Martin Belot

Vincent Gachon

Lucas Vachon

# Project Idea: Equity Portfolio Construction & Stock Selection with ML

This project focuses on applying Machine Learning techniques to the finance sector, specifically for **Equity Portfolio Construction and Optimization**. By leveraging data-driven strategies, we aim to automate and enhance stock selection processes among a given list of stocks (e.g., S&P 500).
 
Implementation of clustering algorithms (Unsupervised Learning) such as *K-Means* or *Hierarchical Clustering* to group stocks with similar characteristics. Usage of clusters to select uncorrelated assets for better portfolio diversification.

We implement a three-step progressive approach to construct the optimal portfolio:

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
