---
layout: post
title: Market State Decoder (Aggressive) - Strategy Prospectus
tags: MarketStateDecoder Prospectus
excerpt_separator:  <!--more-->
---

> _There is nothing permanent except change_ - Heraclitus

This strategy estimates the state in which each security is in, and invests in the securities with the best upside outlook.

The main advantage of this strategy is its ability to provide a significant improvement over the equity markets performance with a relatively low rebalancing frequency.

The main source of risk for this strategy is a period in which the major equity indices continuosly switch state.

#### Strategy details
* Assets: Equity and Government Bonds ETFs
* Backtest period: Jan 2003 - Jan 2021
* Rebalancing frequency: variable, average 4/year
* CAGR: 16.61 %
* Maximum drawdown: 14.52 %
* Sharpe ratio: 1.26
* Leverage: 1
* Detailed tearsheet: [Market State Decoder Aggressive](/tearsheets/market_state_decoder_aggressive.html)

#### Equity curve
Sampling of the equity curve is on a _monthly_ basis. 
![Market State Decoder](/images/market_state_decoder_aggressive.svg)
