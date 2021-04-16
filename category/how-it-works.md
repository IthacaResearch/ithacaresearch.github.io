---
layout: category
title: How it works
sidebar_sort_order: 800
---

## Subscription
The details of all our strategies are public. Please subscribe to one of the plans available on Patreon to receive live updates via e-mail with the latest allocations: [patreon.com/ithaca](https://www.patreon.com/ithaca "Go to Patreon page")

### Sample email
The emails you will receive once subscribed will be in the same format of the one below. If you are not using the strategy already the only relevant information is provided by "Target weights", as your current allocation (weights) is assumed to be zero for all assets. The weights specified in the emails are in the range `[- max leverage, max leverage]`, where the maximum leverage depends on the strategy.

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
All backtests account for transaction fees and slippage, while bid-ask spreads are not taken into account. Orders are always fully filled.

**What is the benchmark displayed in some of the strategies results?**<br>
The benchmark is the S&P 500 index.

**Can the strategies be combined together?**<br>
Absolutely, that is actually how we are currently using them. Please contact us at <info@ithacainvestments.org> if you'd like to review the results of a specific combination of strategies and/or to receive updates for a specific combination.

**Can you provide the trade logs of the backtests?**<br>
Yes, they are available upon request.

**Can you provide further details about the strategies' inner workings?**<br>
We cannot provide the source code of the strategies. However, we can provide the references (our own research notebooks, papers, books, websites) that have inspired the creation of a specific strategy upon request.

**Can a strategy be customized to satisfy specific needs?**<br>
Yes, please contact us at <info@ithacainvestments.org>

**Can you help us implementing and testing a new strategy/idea?**<br>
Yes, please contact us at <info@ithacainvestments.org>

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
