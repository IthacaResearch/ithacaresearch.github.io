---
layout: category
title: How it works
sidebar_sort_order: 800
---

> _There is no favorable wind for the sailor who doesn’t know where to go_ - Seneca

## Introduction
_Ithaca_ is the pool of systematic investment strategies we originally developed to invest our own money. _Ithaca_ has evolved over the years into a platform that runs several automated, systematic investment strategies, and sends emails to the subscribers every time a strategy detects that a rebalance of the portfolio is necessary. An overview of all strategies is [here](/category/strategies).

Systematic investment strategies have several advantages over discretionary ones:
1. investment decisions are not based on emotions
2. the key elements of an investment plan are clearly defined and acted upon: entry criteria, exit criteria, maximum and minimum exposure
3. the actual results can be easily compared to the expected results
4. the investment process can be fully automated
5. it is possible to simulate the execution of a strategy using past data to get an idea of the strategy's characteristics

## Subscription
You can ask for a trial period (maximum three months), or for a quote at <info@ithacainvestments.org>. The only information we need for you to start receiving live updates is a valid email address. You will start receiving updates on the next business day.
The rationale behind each strategy is public and can be found on this website. If you have any questions please [contact us](/category/contacts).

### Sample email
The emails you will receive once subscribed will be in the same format of the one below. If you are not using the strategy already, the only relevant information is provided by "Target weights", as your current allocation (weights) is assumed to be zero for all assets. The weights specified in the emails are in the range `[-max leverage, max leverage]`, where the maximum leverage depends on the strategy.<br>
The email body is in yaml format, so that you could easily parse the message with open source libraries like [PyYAML](https://pyyaml.org/) and execute the trades automatically, for example using [ib_insync](https://github.com/erdewit/ib_insync).

- Subject: ```REBALANCE: StrategyName strategy on 2019-03-03 00:00:00```
- Body:
```yaml
Message:
   Orders sent: true
   Rebalance required for strategies: StrategyName
   Delta weights:   # <--- this is the difference between the current strategy allocation and the target allocation
       TLT: 0.3     # <--- allocate 30% more to TLT, i.e. buy (30% * portfolio value) worth of TLT
       SPY: -0.3    # <--- allocate 30% less to SPY, i.e. sell (30% * portfolio value) worth of SPY
   Current weights: # <--- this is the current strategy allocation (valid only if you are already using the strategy)
       TLT: 0.2
       SPY: 0.8
   Target weights:  # <--- this is the strategy allocation target. The percentage of the assets in your portfolio should match these
       TLT: 0.5
       SPY: 0.5
   Prices:
       TLT: 165.1
       SPY: 314.3
```

## FAQs

**How are the simulated returns calculated?**<br>
Returns are total returns, that is, the backtests assume no withdrawals, and that all distributions (such as dividends) are reinvested in the strategy.

**How realistic are the backtest results?**<br>
All backtests account for transaction fees and slippage, while bid-ask spreads are not taken into account. Orders are simulated as market on close orders and are always fully filled.

**What is the benchmark displayed in some of the strategies results?**<br>
The benchmark is the S&P 500 index.

**Can the strategies be combined together?**<br>
Absolutely, that is actually how we are currently using them. Please [contact us](/category/contacts) if you'd like to review the results of a specific combination of strategies, and/or to receive updates for a custom combination.

**Can you provide the trade logs of the backtests?**<br>
Yes, they are available upon request.

**Can you provide further details about the strategies' inner workings?**<br>
We cannot provide the source code of the strategies. However, we can provide the references (our own research notebooks, papers, books, websites) that have inspired the creation of a specific strategy upon request.

**I'd like to paper-trade the strategies for some time, do you offer a test period?**<br>
Yes, you can receive free updates from the strategies for up to three months before deciding whether or not to subscribe.

**Can a strategy be customized to satisfy specific needs?**<br>
Yes, please [contact us](/category/contacts)

**Can you help us implementing and testing a new strategy/idea?**<br>
Yes, please [contact us](/category/contacts)

**How do I execute the trades?**<br>
To execute the strategies you need to have a brokerage account (some banks provide also brokerage services). The available brokers vary from country to country, as well as the functionalities they provide, the fees they charge, and the products you can trade through them. Here is a list of the most popular brokers:

- [Interactive Brokers](https://www.interactivebrokers.com)
- Fidelity
- Charles Schwab
- Betterment
- TD Ameritrade
- Wealthfront
- Degiro
- Saxo Bank
- Swissquote
