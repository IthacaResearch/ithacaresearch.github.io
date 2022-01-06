---
layout: single
title: Market State Decoder (Defensive, Capped)
subtitle: Strategy Prospectus
permalink: /strategies/market-state-decoder-defensive
excerpt_separator:  <!--more-->
---

> Professionals prepare, amateurs react

This strategy evaluates the "state" in which each portfolio asset is in, and invests in the assets with the best upside outlook.
The "state" of an asset is a quantity determined from several parameters specific to each security, as: volatility, volumes, short and long term trends, correlations with other assets. Once the states have been determined, the portfolio is allocated to the securities with the highest state-wise rank.

The main advantage of this strategy is its ability to provide a significant improvement over the equity markets performance with a relatively low rebalancing frequency.

The main reason of underperformance for this strategy is a period in which the major equity indices continuously switch state (i.e. when equity markets move sideways).

There are three versions of this strategy; the one described on this page is named "defensive" as the allocations to each asset class can never reach 100% of the overall value of the portfolio.

#### Strategy details
* Asset classes: equities, REITs, corporate bonds, government bonds
* Number of assets: 10
* Backtest period: Jan 1998 - Nov 2021
* Rebalancing frequency: monthly
* CAGR: 11.0 %
* Max Drawdown: 11.72 %
* Sharpe ratio: 1.08
* Maximum leverage: 1 (long only)
* Detailed tearsheet: [Market State Decoder Defensive Capped](/tearsheets/MarketStateDecoderDefensiveCapped.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis. 
![Market State Decoder Defensive](/images/MarketStateDecoderDefensiveCapped.svg)
