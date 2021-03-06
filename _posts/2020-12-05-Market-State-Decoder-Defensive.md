---
layout: single
title: Market State Decoder (Defensive)
subtitle: Strategy Prospectus
permalink: /strategies/market-state-decoder-defensive
tags: MarketStateDecoder Prospectus
excerpt_separator:  <!--more-->
---

> _There is nothing permanent except change_ - Heraclitus

This strategy evaluates the "state" in which each portfolio asset is in, and invests in the assets with the best upside outlook.
The "state" of an asset is a quantity determined from several parameters specific to each security, as: volatility, volumes, short and long term trends, correlations with other assets. Once the states have been determined, the portfolio is allocated to the securities with the highest state-wise rank.

The main advantage of this strategy is its ability to provide a significant improvement over the equity markets performance with a relatively low rebalancing frequency.

The main reason of underperformance for this strategy is a period in which the major equity indices continuously switch state (i.e. when equity markets move sideways).

There are two versions of this strategy; the one described on this page is named "defensive" as the allocations to each asset class can never reach 100% of the overall value of the portfolio.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 10
* Backtest period: Jan 1998 - Mar 2021
* Rebalancing frequency: variable, average 4/year
* CAGR: 10.32 %
* Max Drawdown: -12.73 %
* Sharpe ratio: 1.05
* Leverage: 1
* Detailed tearsheet: [Market State Decoder Defensive](/tearsheets/MarketStateDecoderDefensive.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis. 
![Market State Decoder Defensive](/images/MarketStateDecoderDefensive.svg)
