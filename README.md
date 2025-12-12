# **Equity Portfolio Construction & Stock Selection with ML**

**Group 8:** Léo Linossier, Martin Belot, Vincent Gachon, Lucas Vachon

This project focuses on applying Machine Learning techniques to the finance sector, specifically for **Equity Portfolio Construction and Optimization**. By leveraging data-driven strategies, we aim to automate and enhance stock selection processes among a given list of stocks (e.g., S&P 500). Implementation of clustering algorithms (Unsupervised Learning) such as *K-Means* or *Hierarchical Clustering* to group stocks with similar characteristics. Usage of clusters to select uncorrelated assets for better portfolio diversification.

# **Context**

As asset managers for US Life Insurance companies, we seek to optimize the equity allocation of our fund. By leveraging Machine Learning, we aim to select stocks that maximize returns while strictly adhering to the client's low-risk and high-liquidity mandates.

| Client | US Life Insurance Company |
| :--- | :--- |
| **Profile** | Long-term horizon, low risk tolerance, low need for immediate income. |
| **Key Constraints** | **High liquidity requirements** (to cover sudden claims/payouts). |

### **Strategy**

US Life Insurance companies struggle to fund their liabilities: very long-term obligations (10–30 years) often linked to annuity or life insurance contracts, combined with high liquidity needs for claims. Traditional solutions available to insurers (primarily bond portfolios or standardized mixed funds) have shown their limits: they either fail to generate sufficient yield to cover long-term liabilities or take on too much market or liquidity risk, potentially compromising liability stability.

Our fund aims to address this specific need by offering a simple and transparent portfolio that combines **liquidity**, **yield**, and **risk control**. We propose constructing a liquid portfolio, predominantly fixed-income, supplemented by equities (20–25%) to enhance expected returns. This includes quantified yield and volatility targets (rather than guaranteed promises) and quarterly rebalancing to limit risk. This approach would allow the insurer to meet its liquidity and solvency requirements while optimizing the portfolio's long-term return, unlike the standardized solutions currently on the market.

#### Asset Allocation

- **Bonds (70%):** Diversification between Government bonds (e.g., US Treasury 10Y) and Investment Grade Corporate bonds, with a duration focus adapted to liabilities.
- **Equities (30%):** Selection of high-quality US stocks to improve expected yield while limiting volatility (e.g., JPM, 3M, PG).

Quantitative Objectives: Target yield, maximum volatility threshold, minimum liquidity level, with quarterly monitoring to adjust the portfolio according to market evolution.


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


# **Data**

### **Input Data**

SP500 Stock data : $X^{\intercal}=[x^{(1)}, x^{(3)}, ... , x^{(500)}]$

### **Feature Engineering & Selection**

To construct a robust clustering model and optimization engine, we selected features that capture three distinct dimensions of asset behavior: **Market Dynamics**, **Financial Health**, and **Statistical Tail Risk**.

**1) Risk & Return Metrics**

These features quantify how an asset moves relative to itself and the broader market.

- **Return:** Average daily stock returns
- **Realized Volatility:** Annualized standard deviation of daily returns
- **Beta ($\beta$):** Sensitivity to the broader market (e.g., S&P 500)
- **Correlation:** The pairwise correlation of daily returns is often used directly as a "distance" metric for clustering.
- **Momentum:** Returns over the past 3, 6 or 12 months
- **Max drawdown:** The maximum observed percentage decline from a historical peak to a trough. It measures the worst-case scenario for an asset’s value preservation.

**2) Fundamental Ratios**

We incorporate fundamental data to ensure selected stocks possess strong valuation and solvency metrics. These cluster stocks based on their company valuation and financial health.

- **Valuation:** P/E Ratio
- **Profitability:** ROE (Return on Equity)
- **Leverage:** Debt-to-Equity ratio
- **Size:** Market Capitalization

**3) Statistical Moments**

Beyond standard volatility, we examine the distribution of returns to quantify tail risk i.e. the likelihood of rare, extreme negative events

- **Skewness:** Measure of asymmetry in returns distribution.
- **Kurtosis:** Measure of "tail risk" (extreme events).


# **1. K-Means Clustering (Benchmark)**

**Objective**

We utilize K-Means as a baseline algorithm to partition the S&P 500 universe into distinct "risk-return buckets." By grouping stocks with similar characteristics (volatility, liquidity, fundamentals), we can ensure our portfolio diversifies across different behavioral clusters rather than just industrial sectors.

**Algorithm Overview**

K-Means is an iterative algorithm that partitions a dataset of $n$ stocks into $k$ non-overlapping clusters. It aims to minimize the within-cluster sum of squares (variance), ensuring that stocks inside a cluster are as similar as possible.

The objective function $J$ is defined as:

$$J = \sum_{j=1}^{k} \sum_{x_i \in C_j} ||x_i - \mu_j||^2$$

Where:
* $k$ is the number of clusters.
* $C_j$ is the set of points belonging to cluster $j$.
* $\mu_j$ is the centroid (mean) of cluster $j$.
* $||x_i - \mu_j||^2$ is the squared Euclidean distance between a stock $x_i$ and the centroid.

**Implementation Steps**
1.  **Feature Normalization:** All features (e.g., Volatility, P/E, Amihud Ratio) are scaled using Z-Score standardization to prevent large-magnitude features (like Market Cap) from dominating the distance metric.
2.  **Optimal $k$ Selection:** We use the **Elbow Method** and **Silhouette Analysis** to determine the optimal number of clusters that best separates the data without overfitting.
3.  **Cluster assignment:** Stocks are assigned to the nearest cluster centroid based on their feature vector.
4.  **Centroid Update:** The centroids are recalculated as the mean of all stocks in the cluster. Steps 3 and 4 repeat until convergence.



**Application for Insurers**
For our specific client, K-Means helps identify "Defensive Clusters" (low beta, low volatility, high liquidity) vs. "Speculative Clusters." We focus our selection on the most stable clusters to match the insurer's liability constraints.
