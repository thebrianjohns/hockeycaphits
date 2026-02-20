# NHL Player Cap Hit Prediction & Evaluation

**Brian Johns · BrainStation Capstone · April 2022**

---

## Overview

**How accurately can we predict an NHL player's cap hit using their on-ice statistics — and what does the gap between prediction and reality tell us about how teams actually value players?**

This project uses basic and advanced NHL statistics to build regression and clustering models that predict player cap hits, then interprets the results through a sports analytics lens to identify market inefficiencies a front office could exploit.

The three core questions driving the analysis:

1. Which statistics are players currently being *rewarded* for?
2. Which statistics appear *undervalued* — and where are the market gaps?
3. Which players are *over or underpaid* relative to their on-ice contribution?

---

## Data & Tools

- **Source:** [Evolving Hockey](https://evolving-hockey.com) — basic and advanced statistics for all NHL players, 2021–22 season
- **Tools:** Python, Pandas, NumPy, Scikit-Learn, XGBoost, Matplotlib, Seaborn
- **Models:** Lasso Regression, XGBoost Regressor, Random Forest Regressor, PCA, K-Means Clustering

---

## Notebooks

| # | Notebook | Description |
|---|----------|-------------|
| 1 | Data Cleaning & EDA | Data acquisition, cleaning, and exploratory analysis |
| 2 | Preprocessing & Feature Engineering | Scaling, encoding, and feature selection |
| 3 | Modelling | Regression models, PCA, and clustering |
| 4 | Findings | Results, interpretation, and actionable insights |

---

## Key Findings

### What predicts cap hit?

Across all models, the most important features were consistent and revealing:

- **Age** — a major driver of salary, partly due to league contract structures (entry-level caps for rookies) and partly because experience correlates with earning power
- **Overall Draft Pick** — where a player was drafted has a surprisingly persistent effect on salary years later, reflecting long-term expectations baked in at draft time
- **Power Play Time on Ice** — notably, *not* power play production, just the time spent on the ice. Teams are paying for the *expectation* of offensive contribution, not just the results
- **Goals For** — the number of goals scored while a player is on the ice remains the most important production statistic for determining pay

### Best performing model: XGBoost

| Metric | Score |
|--------|-------|
| R² | 0.679 |
| MAE | $0.94M |
| RMSE | $1.29M |

The best model explains **67.9% of cap hit variance** using on-ice statistics alone — meaning roughly one-third of what determines a player's salary cannot be explained by what they do on the ice (leadership, market size, agent quality, and other off-ice factors likely account for much of this gap).

### Undervalued statistics — market gaps for front offices

**Advanced statistics (GAR, WAR)** remain poorly reflected in player salaries despite their growing visibility. Teams that believe advanced metrics are a better measure of true value may still find an edge in targeting players whose advanced numbers outperform their contracts.

**Defensive metrics** in particular show almost no correlation with cap hit. Given how difficult defensive contribution is to measure — and how the market continues to undervalue it — there may be consistent opportunity in players who defend well but don't produce offensively.

### The mega-contract problem

One of the most striking findings: **no model could accurately predict the cap hits of players earning $9M+**. These players were consistently undervalued by the models relative to their actual salary — suggesting that elite players are paid a premium beyond what their statistics justify.

This raises a genuine roster construction question: is one $12.5M player (e.g. Connor McDavid, the best in the game) a better allocation than three $4M players who collectively produce more? The models suggest the latter may be more efficient — though a McDavid-level player affects games in ways statistics don't fully capture.

### Undervalued players

Two consistent categories of undervalued players emerged across all models:

1. **Rookies on entry-level contracts** — players producing at a high level while still on capped rookie deals. Drafting well and developing players quickly maximises this value window.
2. **Veterans on near-minimum deals** — aging players signed cheaply who continue to contribute, particularly those who built strong careers early. The models consistently found these players outperforming their contracts.

Combining these undervalued *player types* with undervalued *statistics* (defensive metrics, advanced stats) points toward a specific market inefficiency: defensively-oriented veterans or late-blooming players whose contributions don't show up in traditional box scores.

### Clustering: player archetypes

K-Means clustering (separated by position) produced interpretable player archetypes:

**Forwards (6 clusters):** Star Forwards · Offensive Producers / Defensive Liabilities · Primary Defensive Forwards · Secondary Defensive Forwards · Fringe NHL Forwards · Enforcers

**Defencemen (4 clusters):** Star Defencemen · Offensive Producers · Defensive Defencemen · Fringe NHL Defencemen

Offensive clusters commanded the highest salaries across both positions, consistent with the regression findings. A notable finding: many players in defensive clusters were earning near-minimum salaries while still contributing meaningfully — reinforcing the defensive value gap identified above.

---

## Future Directions

- Extend the analysis to **team level** — how do the most successful teams construct rosters given these player-level findings?
- Track how **advanced statistics translate to contracts over time** as analytics become more embedded in NHL front offices
- Build **process vs. outcome profiles** comparing expected statistics (xGF, xGA) against actual results — a potentially powerful tool for identifying players who are getting lucky or unlucky relative to their true contribution

---

## Limitations

- Modelling was conducted locally, limiting the scale of hyperparameter tuning available
- The dataset reflects one season (2021–22); multi-year data would produce more robust findings
- Significant unexplained variance (32%) suggests important factors beyond on-ice statistics drive salaries
