# Projet_Data_Finance
Projet du Groupe x 

**Composition du groupe :**

Léo Linossier
Martin Belot
Vincent Gachon
Lucas Vachon


**Project Idea: ML for Autocallable Product Risk Management**

1. Context
	•	Autocallables are structured products, usually linked to equity indices (e.g. EuroStoxx 50), that:
	•	Pay periodic coupons if the underlying stays above a barrier.
	•	Are autocalled (redeemed early) if the underlying is above a certain level on a call date.
	•	Expose the investor to downside risk if the underlying breaches knock-in barriers.
	•	For banks, pricing and risk-managing autocallables is challenging because:
	•	The payoff is highly path-dependent.
	•	Risk exposure (Greeks) is nonlinear and regime-dependent.
	•	Standard models (Black–Scholes, Heston, local vol) may not capture the autocall probability well.

2. ML Angle

The project is about leveraging ML to better estimate risks and behavior of autocallables compared to traditional models.

Possible ML applications: Autocall Probability Estimation
**Train a classifier (logistic regression, random forest, gradient boosting) to estimate the probability of early redemption**


Features for an SP500 Autocall ML Model :

The features should reflect market conditions at observation dates (We want to predict the autocall probability):

A. Spot / Level Features
	•	S_t / K — SP500 spot vs. autocall strike (relative level)
	•	S_t / Barrier — SP500 spot vs. knock-in barrier
	•	Time to Maturity — in years or days
	•	Time to Next Observation — days until next autocall date

B. Volatility Features
	•	Historical Volatility — realized vol over last 20, 60, 120 days
	•	Implied Volatility — ATM 1m, 3m, 6m SPX options if available
	•	Volatility Skew — e.g., IV25d put vs. ATM (proxy for market sentiment)
	•	Volatility Change — difference between current and previous vol measurement

C. Trend / Momentum Features
	•	Return over last N days — e.g., 5d, 20d, 60d returns
	•	Max / Min Drawdown over last N days
	•	Moving Averages — 20d, 50d, 200d

D. Market Regime / Macro Proxies (optional but valuable)
	•	VIX Level — market fear index
	•	SP500 1-day / 5-day volatility
	•	Interest Rate — 3m or 1y Treasury yield
	•	Macro Indicators — optional: e.g., term spread, if available

E. Path-Dependent Features

If you want to capture historical path effects (important for autocall):
	•	Min(S_t) since last observation
	•	Max Drawdown since issuance
	•	Cumulated Returns since issuance


First ML Model to Start With: we just want to predict autocall probability (yes/no).

Model Choice
	•	Logistic Regression → interpretable, fast, baseline.
	•	Output: probability that the autocall will trigger on the next observation date.

Pipeline
	1.	Data preparation
	•	Compute all features above for each observation date in your historical SP500 dataset.
	•	Label: 1 if autocall triggered (spot ≥ strike at observation), else 0.
	2.	Train/test split
	•	Example: train on 2010–2020, test on 2021–2023.
	3.	Model training
