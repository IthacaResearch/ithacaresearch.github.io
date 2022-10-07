---
title: "Global Momentum (Balanced)"
permalink: /strategies/global-momentum-balanced
---

This strategy evaluates a momentum based score for each asset, then ranks the assets within the same category according to their scores, and invests in equal parts in the highest ranking assets in each category.

Assets are grouped in three categories: risky assets (for example equities), safe assets (for example government bonds), and risk-free assets (for example ultra short term government bonds). If there is no asset with a positive score in a given category, the corresponding part of the portfolio will be allocated to the highest ranking risk-free assets.

The main source of underperformance for this strategy is the same as for the "Aggressive" variant: a lack of a clear trend across different asset classes. The higher diversification helps reducing this problem though.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 25
* Backtest period: Jan 1998 - Jan 2022
* Rebalancing frequency: monthly
* CAGR: 13.69 %
* Max Drawdown: -19.76 %
* Sharpe ratio: 1.15
* Maximum leverage: 1 (long only)
* Detailed tearsheet: [Global Momentum Balanced](/tearsheets/GlobalMomentumBalanced.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis.

![Global Momentum](/images/GlobalMomentumBalanced.svg)
