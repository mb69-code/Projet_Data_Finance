# Scripts

### eda.ipynb

This notebook constructs and presents the dataset used throughout the project and includes an exploratory data analysis to better understand its characteristics. The analysis covers:

- **General Information and Statistics:** Using `info()` and `describe()` to examine the structure and summary statistics of the dataset.  
- **Risk vs. Reward Analysis:** Plotting *Volatility* against *Momentum*, scaled by market capitalization, to identify patterns in the 2022–2024 period.  
- **Correlation Analysis:** Checking relationships between features and assessing multicollinearity.  
- **Outlier Detection and Feature Distributions:** Identifying extreme values and distribution shapes to determine the preprocessing steps required for clustering.

### efficient-frontier-benchmark.ipynb

This notebook focuses on constructing the optimal portfolio using Modern Portfolio Theory (Markowitz) by maximizing the Sharpe ratio. It serves as a benchmark to evaluate the performance of stock selection methods implemented with machine learning techniques, such as clustering and genetic algorithms.  

The approach represents the conventional method for portfolio construction, aiming to balance expected returns and risk (volatility). It uses only two features: annualized volatility and returns. The notebook is still under development, and at this stage, a test has been conducted using a subset of 10 stocks from the S&P500.

### k-means.ipynb

This notebook implements the K-Means algorithm as a benchmark machine learning method. It uses the 9-feature dataset prepared in `eda.ipynb` and applies the necessary preprocessing steps to ensure the data is suitable for clustering.  

The goal is to classify stocks into distinct market regimes based on both risk and fundamental metrics. By analyzing the resulting clusters, we can identify patterns such as groups of low-volatility, high-momentum large caps versus high-risk, high-variance small caps. These clusters will later be compared with portfolios constructed using alternative techniques, like the genetic algorithm, to assess their effectiveness in capturing market structure.
