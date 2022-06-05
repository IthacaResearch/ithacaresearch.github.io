---
title: "An implementation of 'Deep Learning for Portfolio Optimization' by Zhang, Z. , Zohren, S. , Roberts, S."
excerpt: "Can a diversified portfolio built using a deep learning model trained on price data beat the risk adjusted returns of the market? The short answer is: no."
---

_Can a diversified portfolio built using a deep learning model trained on price data beat the risk adjusted returns of the market? The short answer is: no._

## Introduction

The article "[Deep Learning for Portfolio Optimization](https://arxiv.org/pdf/2005.13665.pdf)" proposes an interesting approach to building a diversified portfolio using highly liquid Exchange Traded Funds (ETFs): a deep learning model is trained and used to obtain the portfolio weights which optimize the portfolio Sharpe ratio.

The results shown in the article are promising, and the possibility to have the model directly spitting out the optimal weights is enticing. The major issue we have found with the article is the following:

> We use four market indices: US total stock index (VTI), US aggregate bond index (AGG), US commodity index (DBC) and Volatility Index (VIX).

The [VIX](https://www.cboe.com/tradable_products/vix/faqs/) is an index, not an investable asset, and therefore the results included in the article could never be achieved by an actual portfolio as there are no financial instruments that replicate the performance of the VIX. We could surely use VIX futures, VIX future options, or ETPs based on VIX futures, but none of these track the VIX well. Why is this the case? Read [this](https://sixfigureinvesting.com/2010/01/how-to-go-long-on-the-vix-index-2/) and [this](https://sixfigureinvesting.com/2013/08/trading-the-vix-index/).

## Replicating the results

Although the performance of the strategy reported in the article cannot be actually replicated, we have benchmarked our implementation by using market data very similar to the one used by the authors. The source code shows [VXX](https://finance.yahoo.com/quote/VXX) (which is a listed instrument) as the instrument tracking the VIX, but its market data has been replaced with the [VIX](https://finance.yahoo.com/quote/^VIX) historical data to replicate the results of the article.

The performance of our implementation is similar to the performance reported in the original article. The detailed reports are below.

- Backtest results (no target volatility): [No target volatility](/notebooks/dlpopt_no_target_vol.html)
- Backtest results (annualized target volatility = 10%): [Target volatility 10%](/notebooks/dlpopt_target_vol_10.html)

## Alternative strategies

The results reported in the article cannot be replicated in an actual portfolio, but since the methodology seems promising we have tried applying it to investable assets only. Specifically, we have run different simulation using the following sets of assets:

A) [SPY](https://finance.yahoo.com/quote/SPY), [GHAAX](https://finance.yahoo.com/quote/GHAAX), [VWESX](https://finance.yahoo.com/quote/VWESX), [VUSTX](https://finance.yahoo.com/quote/VUSTX)

B) [SPY](https://finance.yahoo.com/quote/SPY), [GHAAX](https://finance.yahoo.com/quote/GHAAX), [AGG](https://finance.yahoo.com/quote/VWESX), [DFIHX](https://finance.yahoo.com/quote/DFIHX)

C) [SPY](https://finance.yahoo.com/quote/SPY), [GHAAX](https://finance.yahoo.com/quote/GHAAX), [AGG](https://finance.yahoo.com/quote/AGG), [VIXY](https://finance.yahoo.com/quote/VIXY)

D) [SPY](https://finance.yahoo.com/quote/SPY), [GHAAX](https://finance.yahoo.com/quote/GHAAX), [AGG](https://finance.yahoo.com/quote/AGG), [SH](https://finance.yahoo.com/quote/SH)

Using mutual funds allows us to run a longer simulation as some of them have been trading since the eighties, and market data therefore starts earlier on.<br>
Trading is simulated at the close (this causes a positive skew in the simulated performance, but the effect can be neglected for the sake of comparison with the strategy reported in the original article).<br>
Transaction costs are simulated by the broker implementation in the Lean backtesting engine.

## Results

The simulated performance of the methodology proposed in the original article is unfortunately poor when using investable assets. The results for each simulation are below.

### Portfolio A
- Assets: SPY, GHAAX, VWESX, VUSTX
- Rebalancing: daily
- Training: every 2 years
- Target volatility: no
- Performance
    - Sharpe ratio: 0.69
    - CAGR: 10.08 %
    - Max drawdown: -33.75 %
- [Detailed tearsheet](/notebooks/dlpopt_daily_spy_ghaax_vustx_vwesx.html)

### Portfolio B

### Portfolio C

### Portfolio D

## Source code (Python)

Model implementation:

```python
import gc
import numpy as np
np.random.seed(11)
import pandas as pd

import tensorflow as tf
import tensorflow.keras.backend as K
from tensorflow.keras.layers import LSTM, Flatten, Dense
from tensorflow.keras.models import Sequential
from tensorflow.keras.callbacks import Callback
from keras.preprocessing.sequence import TimeseriesGenerator
from keras.callbacks import EarlyStopping

tf.config.threading.set_intra_op_parallelism_threads(6)
tf.config.threading.set_inter_op_parallelism_threads(6)


class DeepLearningPortfolioOptimizationModel:

    def __init__(self, target_annualized_volatility = 10.,
                 run_eagerly = True,
                 save_prediction_history = False,
                 test_len = 50,
                 batch_size = 64,
                 retrain_every_months = 24,
                 n_epochs = 100):

        self.target_annualized_volatility = target_annualized_volatility
        self.run_eagerly = run_eagerly
        self.save_prediction_history = save_prediction_history
        self.test_len = test_len
        self.retrain_every_months = retrain_every_months
        self.n_epochs = n_epochs
        self.batch_size = batch_size

        self.idx = 0
        self.counter = 0
        self.model = None
        self.history = None
        self.callbacks = None
        return


    def get_weights(self, data):
        """ Return the optimal portfolio weights on the basis of the historical data available """

        # Clear model at every call
        if self.retrain_every_months < 0:
            self.model = None
        # Clear model after a given number of iterations
        if self.counter % self.retrain_every_months == 0:
            self.model = None
        self.counter += 1

        def custom_loss_wrapper(dfs):
            """ Wrap the loss function to be able to feed a different dataframe for each step """

            def sharpe_loss(y_true, y_pred):
                """ Loss function which minimizes -sharpe_ratio (maximizes Sharpe) """

                df = dfs[self.idx]
                tfData = tf.cast(tf.constant(df), float)
                portfolio_returns = (tfData[1:] / tfData[:-1]) - 1
                if self.target_annualized_volatility > 0:
                    std = tf.cast(tf.constant(self.target_annualized_volatility / (df[-self.test_len:].dropna().pct_change().dropna().ewm(com=0.5).std()[-1:] * np.sqrt(252) * 100)), float)
                    portfolio_returns = tf.reduce_sum(tf.multiply(portfolio_returns, tf.multiply(std, y_pred)), axis = 1)
                else:
                    portfolio_returns = tf.reduce_sum(tf.multiply(portfolio_returns, y_pred), axis = 1)

                mean = K.mean(portfolio_returns)
                std = K.std(portfolio_returns)
                self.idx += 1
                return -mean / std

            return sharpe_loss

        # Concatenate prices and returns
        dataset = np.concatenate([data.values[1:], data.pct_change().values[1:]], axis = 1)
        # Build a mock target dataset
        y_train = [np.ones((1, len(data.columns))) * 1. / len(data.columns) for i in range(0, len(dataset))]
        n_features = dataset.shape[1]

        # Prepare the input for the prediction
        x_pred = dataset[-self.test_len:]
        x_pred = x_pred.reshape((1, self.test_len, n_features))
        callbacks = []

        # Train the network if the model has been cleared
        if not self.model:
            
            # Prepare the data necessary for training
            self.idx = 0
            generator = TimeseriesGenerator(dataset, y_train, length = self.test_len, shuffle = False, batch_size = self.batch_size)
            dfs = [data[i:i + self.batch_size + 1] for i in range(generator.start_index, generator.end_index, generator.batch_size)]

            # Define the model
            self.model = Sequential([
                    LSTM(64, input_shape = (self.test_len, n_features)),
                    Flatten(),
                    Dense(len(data.columns), activation = 'softmax')
                    ])
            optimizer = tf.keras.optimizers.Adam(amsgrad = False)
            loss = custom_loss_wrapper(dfs)
            self.model.compile(loss = loss, optimizer = optimizer, run_eagerly = self.run_eagerly)

            # Add custom callbacks
            callbacks.append(ResetIndexCallback(self))
            if self.run_eagerly:
                callbacks.append(ClearMemory())
            if self.save_prediction_history:
                callbacks.append(PredictionHistoryCallback(x_pred))

            # Train the model
            steps_per_epoch = int(len(dataset) / float(self.batch_size)) - 1
            self.history = self.model.fit(generator, shuffle = False, steps_per_epoch = steps_per_epoch, epochs = self.n_epochs, verbose = 0, batch_size = self.batch_size,
                                          callbacks = callbacks)

        # Predict portfolio weights and return all results
        prediction = self.model.predict(x_pred, verbose = 0)
        predictionResults = PredictionResults(self.model, self.history, prediction, callbacks)
        return predictionResults


class ClearMemory(Callback):
    def on_epoch_end(self, epoch, logs = None):
        gc.collect()
        K.clear_session()


class PredictionHistoryCallback(Callback):
    def __init__(self, x_test):
        self.x_test = x_test
        self.prediction_history = list()

    def on_epoch_end(self, epoch, logs = None):
        self.prediction_history.append(self.model.predict(self.x_test))


class ResetIndexCallback(Callback):
    def __init__(self, model_container):
        self.model_container = model_container
        self.n_epochs = 0
        return

    def on_epoch_end(self, epoch, logs = None):
        self.n_epochs += 1
        self.model_container.idx = 0


class PredictionResults():
    def __init__(self, model, history, prediction, callbacks):
        self.model = model
        self.history = history
        self.prediction = prediction
        self.weights = prediction[0]
        self.callbacks = callbacks
        return

```

Backtest code:

```python
from QClibs import *
from System import *

import numpy as np
np.random.seed(11)
from collections import OrderedDict, deque

from DLPOM import DeepLearningPortfolioOptimizationModel


class DeepLearningPortfolioOptimizationAlgo(QCAlgorithm):

    def Initialize(self):
        self.SetStartDate(2012, 1, 1)
        self.SetCash(1e6)

        # tickers = ['VTI', 'DBC', 'VGK', 'VPL', 'EEM', 'GLD', 'TLT', 'IEF', 'QQQ', 'VNQ', 'VB', 'TIP', 'LQD']
        # tickers = ['SPY', 'GHAAX', 'VWESX', 'VUSTX']
        # tickers = ['VTI', 'DBC', 'AGG', 'VXX']
        tickers = ['SPY', 'GHAAX', 'VBMFX', 'VXX']

        for t in tickers:
            self.AddEquity(t, Resolution.Daily)

        for s in self.Securities.Values:
            s.SetDataNormalizationMode(DataNormalizationMode.SplitAdjusted)

        self.target_annualized_volatility = -1
        self.train_period = 5 * 252
        self.data = deque(maxlen = self.train_period*10)
        self.model = DeepLearningPortfolioOptimizationModel(target_annualized_volatility = -1.,
                                                            test_len = 50,
                                                            retrain_every_months = 24,
                                                            n_epochs = 100,
                                                            batch_size = 64,
                                                            run_eagerly = True,
                                                            save_prediction_history = False)

        self.Train(self.DateRules.MonthStart(tickers[0]), self.TimeRules.BeforeMarketClose(tickers[0]), self.Rebalance)
        self.SetWarmup(self.train_period)

        self.SetBrokerageModel(BrokerageName.InteractiveBrokersBrokerage, AccountType.Margin)

        self.last_weights = None
        self.previous_day = -1
        return


    def Rebalance(self):

        # Not enough data yet
        if len(self.data) < self.train_period:
            self.Debug(f'{self.Time} - data not ready')
            return

        # Convert the list of Slices into a single dataframe
        try:
            data = self.PandasConverter.GetDataFrame(list(self.data)).iloc[::-1]
        except Exception as ex:
            self.Error(f'{self.Time} - could not convert dataframe: {ex}')
            return

        # Extract the close prices
        data = data['close'].unstack(level = 0).dropna()
        tickers = [s.split(' ')[0] for s in data.columns]

        # Get the optimal weights
        prediction_results = self.model.get_weights(data)
        weights = prediction_results.weights

        # Check if weights are valid
        if any(np.isnan(weights)):
            self.Error(f"Orders will not be sent as some weights are not valid: {weights}")
            return
        if weights is None or len(weights) == 0:
            self.Error(f'{self.Time} - Portfolio weights are not valid: {weights}')
            return
        
        # Volatility targeting
        if self.target_annualized_volatility > 0:
            vol = np.minimum(1, self.target_annualized_volatility/data.pct_change().dropna().ewm(com=0.5).std()[-1:] * np.sqrt(252) * 100)
            weights = (weights * vol).values[0]

        self.Log(f'{self.Time} - Portfolio weights: {weights}')

        # Order target portfolio weights in ascending order to be sure that sell orders are sent before buy orders
        delta_weights = []
        if self.last_weights is not None and len(self.last_weights) == len(weights):
            delta_weights = [w - l for l, w in zip(self.last_weights, weights)]
            ticker_weight = sorted(zip(tickers, weights, delta_weights), key = lambda x: x[2], reverse = False)
        else:
            ticker_weight = sorted(zip(tickers, weights, weights), key = lambda x: x[1], reverse = False)

        # Send orders
        # if not delta_weights or (delta_weights and any([abs(d)>2.5/100. for d in delta_weights])):
        for t, w, dw in ticker_weight:
            if dw > 0:
                self.SetHoldings(t, w * 0.99)
            else:
                self.SetHoldings(t, w)

        self.last_weights = weights

        return


    def OnData(self, data):
        if self.previous_day != self.Time.day:
            self.data.appendleft(data)
        self.previous_day = self.Time.day
        return
```

Lean engine dependencies:

```python
from QuantConnect import *
from QuantConnect.Parameters import *
from QuantConnect.Benchmarks import *
from QuantConnect.Brokerages import *
from QuantConnect.Util import *
from QuantConnect.Interfaces import *
from QuantConnect.Algorithm import *
from QuantConnect.Algorithm.Framework import *
from QuantConnect.Algorithm.Framework.Selection import *
from QuantConnect.Algorithm.Framework.Alphas import *
from QuantConnect.Algorithm.Framework.Portfolio import *
from QuantConnect.Algorithm.Framework.Execution import *
from QuantConnect.Algorithm.Framework.Risk import *
from QuantConnect.Indicators import *
from QuantConnect.Data import *
from QuantConnect.Data.Consolidators import *
from QuantConnect.Data.Custom import *
from QuantConnect.Data.Fundamental import *
from QuantConnect.Data.Market import *
from QuantConnect.Data.UniverseSelection import *
from QuantConnect.Notifications import *
from QuantConnect.Orders import *
from QuantConnect.Orders.Fees import *
from QuantConnect.Orders.Fills import *
from QuantConnect.Orders.Slippage import *
from QuantConnect.Scheduling import *
from QuantConnect.Securities import *
from QuantConnect.Securities.Equity import *
from QuantConnect.Securities.Forex import *
from QuantConnect.Securities.Interfaces import *
from datetime import date, datetime, timedelta
from QuantConnect.Python import *
from QuantConnect.Storage import *
QCAlgorithmFramework = QCAlgorithm
QCAlgorithmFrameworkBridge = QCAlgorithm
```
