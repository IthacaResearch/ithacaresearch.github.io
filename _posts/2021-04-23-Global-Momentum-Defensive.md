---
title: "Global Momentum (Defensive)"
categories:
  - "Strategy Prospectus"
---

This strategy evaluates a Sharpe ratio based score for each asset, then ranks the assets within the same category according to their scores, and invests in equal parts in the highest ranking assets in each category.

Assets are grouped in three categories: risky assets (for example equities), safe assets (for example government bonds), and risk-free assets (for example ultra short term government bonds). If there is no asset with a positive score in a given category, the corresponding part of the portfolio will be allocated to the highest ranking risk-free assets.

This strategy leverages an even broader diversification than its "aggressive" variant, and focuses on increasing the predictability of the returns rather than maximizing the returns themselves.

The main source of underperformance for this strategy is the same as for its "aggressive" variant: a lack of a clear trend across different asset classes. Compared to the other variant though, the broader diversification helps reducing this problem.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 25
* Backtest period: Jan 1998 - May 2021
* Rebalancing frequency: monthly
* CAGR: 12.01 %
* Max Drawdown: -15.91 %
* Sharpe ratio: 1.32
* Leverage: 1
* Detailed tearsheet: [Global Momentum Defensive](/tearsheets/GlobalMomentumDefensive.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis.

![Global Momentum](/images/GlobalMomentumDefensive.svg)
