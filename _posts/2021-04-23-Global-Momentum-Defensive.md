---
title: "Global Momentum (Defensive)"
permalink: /strategies/global-momentum-defensive
---

This strategy evaluates a Sharpe ratio based score for each asset, then ranks the assets within the same category according to their scores, and invests in equal parts in the highest ranking assets in each category.

Assets are grouped in three categories: risky assets (for example equities), safe assets (for example government bonds), and risk-free assets (for example ultra short term government bonds). If there is no asset with a positive score in a given category, the corresponding part of the portfolio will be allocated to the highest ranking risk-free assets.

This strategy is the most broadly diversified of the Global Momentum family, and focuses on maximizing the predictability of the returns rather than the returns.

The main source of underperformance for this strategy is the same as for its "aggressive" variant: a lack of a clear trend across different asset classes. This stategy's broader diversification helps in limiting the impact of this scenario.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 25
* Backtest period: Jan 1998 - Sep 2021
* Rebalancing frequency: monthly
* CAGR: 11.53 %
* Max Drawdown: -16.83 %
* Sharpe ratio: 1.28
* Maximum leverage: 1 (long only)
* Detailed tearsheet: [Global Momentum Defensive](/tearsheets/GlobalMomentumDefensive.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis.

![Global Momentum](/images/GlobalMomentumDefensive.svg)
