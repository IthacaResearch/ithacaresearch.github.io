---
title: "Global Momentum (Aggressive)"
permalink: /strategies/global-momentum-aggressive
---

This strategy evaluates a momentum based score for each asset, then ranks the assets within the same category according to their scores, and invests in equal parts in the highest ranking assets in each category.

Assets are grouped in three categories: risky assets (for example equities), safe assets (for example government bonds), and risk-free assets (for example ultra short term government bonds). If there is no asset with a positive score in a given category, the corresponding part of the portfolio will be allocated to the highest ranking risk-free assets.

The main advantage of this strategy is its ability to avoid major equity markets downtrends through diversification and momentum filtering.

The main source of underperformance for this strategy is the lack of a clear trend across different asset classes.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 25
* Backtest period: Jan 1998 - Oct 2022
* Rebalancing frequency: monthly
* CAGR: 15.33 %
* Max Drawdown: 26.12 %
* Sharpe ratio: 1.14
* Maximum leverage: 1 (long only)
* Detailed tearsheet: [Global Momentum Aggressive](/tearsheets/GlobalMomentumAggressive.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis.

![Global Momentum](/images/GlobalMomentumAggressive.svg)
