# BTC/USDT Market Predictive Models

This repository contains the implementation of SARIMA-based and LSTM-based predictive models for algorithmic trading in the BTC/USDT market. The project was developed as part of a hackathon where we built machine learning models to predict BTC/USDT prices and implemented trading strategies based on these predictions.

## Table of Contents

- [Introduction](#introduction)
- [Data Preprocessing](#data-preprocessing)
- [SARIMA Model](#sarima-model)
- [LSTM Model](#lstm-model)
- [Backtesting and Results](#backtesting-and-results)
- [Risk Management](#risk-management)
- [Contributors](#contributors)
- [License](#license)

## Introduction

The aim of this project is to develop predictive models for BTC/USDT market prices and utilize these predictions to implement effective trading strategies. We used two approaches:
1. **SARIMA Model**: To capture the temporal dependencies in the BTC/USDT time series data.
2. **LSTM Model**: To leverage deep learning for more complex pattern recognition and prediction.

## Data Preprocessing

The dataset used consists of OHLC (Open, High, Low, Close) data from 2018-01-01 to 2022-01-31, with a 6-hour interval. The preprocessing steps included:
- Selecting the 'Close' column for analysis.
- Checking stationarity using the Dickey Fuller test.
- Applying STL Decomposition for seasonal differencing.
- Stabilizing variance with Box Cox transformation.

## SARIMA Model

### Implementation
- **Model Parameters**: (p=2, d=1, q=4, P=0, D=1, Q=1, s=24).
- **Grid Search**: Performed to find the best parameters based on AIC.
- **Time Aware Cross Validation**: 20 folds with MAPE as the evaluation metric.

### Forecasting
- Predictions were transformed back using inverse Box Cox transformation.
- Trading strategy based on moving averages (78-hour > 144-hour for buy, 78-hour < 144-hour for sell).

## LSTM Model

### Implementation
- **Data Features**: Included additional features like High-Low ratio, Daily Returns, Moving Averages, and RSI to prevent overfitting.
- **Model Structure**: 2 Bidirectional LSTM layers with 128 and 64 units, recurrent dropouts, and a Dense layer.
- **Optimization**: Used RMSProp and Adam optimizers with mean squared error loss.

### Forecasting
- The model takes the last 30-minute time series data as input.
- Predictions were made using a sliding window approach.

## Backtesting and Results

### SARIMA Model
- **Performance Metrics**: Sharpe Ratio: 1.1299, Annualized Returns: 10.16%, Maximum Drawdown: 7.92%.
- **Equity Curve Analysis**: Demonstrates effective buy/sell signal generation based on predicted prices.

### LSTM Model
- **Performance Metrics**: MAPE on test data around 0.18%-0.20%.
- **Equity Curve Analysis**: Accurate prediction of buy/sell signals based on moving averages.

## Risk Management

- **Stop Loss**: Set at 0.02 with a reward-risk ratio of 2:1.
- Performance metrics like Sharpe Ratio, annualized returns, and maximum drawdown were calculated to evaluate the risk.

## Contributors

- [Abhirup Adhikary](https://github.com/AbhiZx18324)
- [Ayanak Misra](https://github.com/Ayanak2004)
