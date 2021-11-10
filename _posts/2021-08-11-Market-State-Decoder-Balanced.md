---
layout: single
title: Market State Decoder (Balanced)
subtitle: Strategy Prospectus
permalink: /strategies/market-state-decoder-balanced
excerpt_separator:  <!--more-->
---

This strategy evaluates the "state" in which each portfolio asset is in, and invests in the assets with the best upside outlook.
The "state" of an asset is a quantity determined from several parameters specific to each security, as: volatility, volumes, short and long term trends, correlations with other assets. Once the states have been determined, the portfolio is allocated to the securities with the highest state-wise rank.

The main advantage of this strategy is its ability to provide a significant improvement over the equity markets performance with a relatively low rebalancing frequency.

The main reason of underperformance for this strategy is a period in which the major equity indices continuously switch state (i.e. when equity markets move sideways).

There are three versions of this strategy. The one described on this page is named "balanced" as the allocations to each asset class can never reach 100% of the overall value of the portfolio, but the overall diversification is lower than the "defensive" variant of this strategy.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 10
* Backtest period: Jan 1998 - Nov 2021
* Rebalancing frequency: variable, average 4/year
* CAGR: 12.05 %
* Max Drawdown: 13.52 %
* Sharpe ratio: 0.99
* Leverage: 1
* Detailed tearsheet: [Market State Decoder Balanced](/tearsheets/MarketStateDecoderBalanced.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis. 
![Market State Decoder Balanced](/images/MarketStateDecoderBalanced.svg)
