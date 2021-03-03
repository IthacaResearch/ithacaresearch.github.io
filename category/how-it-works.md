---
layout: category
title: How it works
sidebar_sort_order: 800
---

## Subscription
The details of all our strategies are public. Please subscribe to one of the plans available on Patreon to receive live updates via e-mail with the latest allocations: [patreon.com/ithaca](https://www.patreon.com/ithaca "Go to Patreon page")

### Sample email
The emails you will receive once subscribed will be in the same format of the one below. If you are not using the strategy already, the only relevant information is provided by "Target weights", as your current allocation (weights) is zero for all assets.

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
   Target weights:  # <--- this is the strategy allocation target
       TLT: 0.5
       SPY: 0.5
   Prices:
       TLT: 165.1
       SPY: 314.3
```

## Execution
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
