---
title: Market State Decoder (Aggressive)
tags: MarketStateDecoder Prospectus
excerpt_separator:  <!--more-->
---

> _There is nothing permanent except change_ - Heraclitus

This strategy evaluates the "state" in which each portfolio asset is in, and invests in the assets with the best upside outlook.
The "state" of an asset is a quantity determined from several parameters specific to each security, as: volatility, volumes, short and long term trends, correlations with other assets. Once the states have been determined, the portfolio is allocated to the securities with the highest state rank.

The main advantage of this strategy is its ability to provide a significant improvement over the equity markets performance with a relatively low rebalancing frequency.

The main reason of underperformance for this strategy is a period in which the major equity indices continuosly switch state (i.e. when equity markets move sideways).

There are two versions of this strategy; the one described on this page is named "aggressive" as the allocations to each asset class can reach 100% of the overall value of the portfolio.

#### Strategy details
* Asset classes: equities, government bonds
* Number of assets: 6
* Backtest period: Jan 1998 - Jan 2021
* Rebalancing frequency: variable, average 4/year
* CAGR: 14.17 %
* Max Drawdown: -19.8 %
* Sharpe ratio: 0.98
* Leverage: 1
* Detailed tearsheet: [Market State Decoder Aggressive](/tearsheets/market_state_decoder_aggressive.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis. 
![Market State Decoder](/images/market_state_decoder_aggressive.svg)
