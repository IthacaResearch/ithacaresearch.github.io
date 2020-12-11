---
layout: post
title: Market State Decoder - Strategy Prospectus
tags: MarketStateDecoder Prospectus
excerpt_separator:  <!--more-->
---

> _There is nothing permanent except change_ - Heraclitus

This strategy estimates the state in which each security is in, and invests in the securities with the best upside outlook.

The main advantage of this strategy is its ability to provide a significant improvement over the equity markets performance with a relatively low rebalancing frequency.

The main source of risk for this strategy is a period in which the major equity indices continuosly switch state.

#### Strategy details
* Assets: Equity and Government Bonds ETFs
* Backtest period: Jan 2003 - Dec 2020
* Rebalancing frequency: variable, average 4/year
* CAGR: 15.47 %
* Maximum drawdown: 16.48 %
* Sharpe ratio: 1.16
* Leverage: 1
* Detailed tearsheet: [Market State Decoder](/tearsheets/market_state_decoder.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis. 
![Market State Decoder](/images/market_state_decoder.svg)
