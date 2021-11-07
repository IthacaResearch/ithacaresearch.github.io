---
title: "Global Momentum (Balanced)"
permalink: /strategies/global-momentum-balanced
---

This strategy evaluates a Sharpe ratio based score for each asset, then ranks the assets within the same category according to their scores, and invests in equal parts in the highest ranking assets in each category.

Assets are grouped in three categories: risky assets (for example equities), safe assets (for example government bonds), and risk-free assets (for example ultra short term government bonds). If there is no asset with a positive score in a given category, the corresponding part of the portfolio will be allocated to the highest ranking risk-free assets.

This strategy is the most broadly diversified of the Global Momentum family, and focuses on maximizing the predictability of the returns rather than the returns.

The main source of underperformance for this strategy is the same as for the "aggressive" variant: a lack of a clear trend across different asset classes. The higher diversification helps reducing this problem though.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 25
* Backtest period: Jan 1998 - Nov 2021
* Rebalancing frequency: monthly
* CAGR: 13.9 %
* Max Drawdown: -19.13 %
* Sharpe ratio: 1.13
* Leverage: 1
* Detailed tearsheet: [Global Momentum Defensive](/tearsheets/GlobalMomentumBalanced.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis.

![Global Momentum](/images/GlobalMomentumBalanced.svg)
