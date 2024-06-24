# Dynamic Pairs Trading Strategy: MRVL vs MU

## Table of Contents
1. [Introduction](#introduction)
2. [Features](#features)
3. [Strategy Details](#strategy-details)
4. [Data Acquisition](#data-acquisition)
5. [Statistical Analysis](#statistical-analysis)
6. [Backtesting](#backtesting)
7. [Performance Metrics](#performance-metrics)
8. [Visualization](#visualization)
9. [Limitations and Risks](#limitations-and-risks)
10. [Future Improvements](#future-improvements)
11. [License](#license)

## Introduction

This repository contains a Python implementation of a dynamic pairs trading strategy for Marvell Technology (MRVL) and Micron Technology (MU) stocks. The strategy leverages statistical arbitrage techniques, primarily based on the z-score of the spread between the two assets' prices. It includes comprehensive data fetching, statistical analysis, strategy development, backtesting, and performance evaluation components.

## Features

- Dynamic pairs trading strategy based on z-score analysis
- Real-time data fetching from Polygon.io API
- Statistical tests for stationarity and cointegration
- Advanced backtesting using VectorBT
- Comprehensive performance analysis and visualization
- Adaptive entry and exit thresholds

## Strategy Details

The strategy employs a dynamic approach to pairs trading:

1. Calculates the spread between MRVL and MU prices
2. Computes the z-score of this spread
3. Uses rolling standard deviations to determine dynamic entry and exit thresholds
4. Enters a position when the z-score exceeds the entry threshold
5. Exits the position when the z-score reverts to the exit threshold

Key parameters:
- Entry threshold multiplier: 2
- Exit threshold multiplier: 1
- Rolling window for standard deviation: 20 days

## Data Acquisition

Historical price data is fetched using the Polygon.io API. The script includes functions to retrieve:
- Daily OHLCV data
- Daily open prices

Data is aligned and preprocessed to handle any missing values or discrepancies.

## Statistical Analysis

The script performs several statistical tests:

# Augmented Dickey-Fuller (ADF) test for stationarity on:
- Price series
- Returns series
- Log returns series

### Price Series
$$
\Delta r_t = \alpha + \beta t + \gamma r_{t-1} + \sum_{i=1}^{p} \delta_i \Delta r_{t-i} + \epsilon_t
$$

### Returns Series
$$
\Delta r_t = \alpha + \beta t + \gamma r_{t-1} + \sum_{i=1}^{p} \delta_i \Delta r_{t-i} + \epsilon_t
$$

### Log Returns Series
$$
\Delta \ell_t = \alpha + \beta t + \gamma \ell_{t-1} + \sum_{i=1}^{p} \delta_i \Delta \ell_{t-i} + \epsilon_t
$$

# Augmented Engle-Granger test for cointegration

### Step 1: Estimate the Cointegrating Regression
$$
y_t = \alpha + \beta x_t + u_t
$$

### Step 2: Test for Stationarity of the Residuals

$$
\Delta \hat{u}_t = \gamma \hat{u}_{t-1} + \sum_{i=1}^{p} \delta_i \Delta \hat{u}_{t-i} + \epsilon_t
$$


# Linear Regression to Determine the Relationship Between MRVL and MU Prices

Let \( P_{MRVL} \) be the price of Marvell Technology Group Ltd. (MRVL) and \( P_{MU} \) be the price of Micron Technology, Inc. (MU). The linear regression model can be represented as:

$$
P_{MRVL} = \alpha + \beta P_{MU} + \epsilon
$$

Where:
- \( \alpha \) is the intercept of the regression line.
- \( \beta \) is the slope of the regression line, representing the relationship between MRVL and MU prices.
- \( \epsilon \) is the error term.



These tests provide insights into the statistical properties of the asset pair and help validate the strategy's assumptions.

## Backtesting

The strategy is backtested using VectorBT, a powerful library for high-performance backtesting. Key aspects of the backtesting process include:

- Initial capital: $100,000
- Trading fees: 0.1% per trade
- Position sizing: 100% of available capital for each asset
- Cash sharing between assets
- Daily rebalancing

## Performance Metrics

The backtest results (as of the last run) show:

- Total Return: 521.51%
- Benchmark Return: 142.38%
- Sharpe Ratio: 1.52
- Calmar Ratio: 1.89
- Sortino Ratio: 2.59
- Max Drawdown: 42.13%
- Win Rate: 67.39%
- Total Trades: 48
- Profit Factor: 2.38

## Visualization

The script generates various plots using Plotly:

1. Price comparison of MRVL and MU
2. Z-score time series with trading signals
3. Scatter plots of prices and returns
4. Equity curve
5. Drawdown analysis
6. Trade analysis

These visualizations provide intuitive insights into the strategy's performance and behavior.

## Limitations and Risks

- The strategy's performance may be sensitive to the chosen parameters
- Past performance does not guarantee future results
- The approach assumes a consistent statistical relationship between MRVL and MU
- Large drawdowns may occur, as evidenced by the 42.13% maximum drawdown in the backtest

## Future Improvements

1. Implement additional risk management techniques (e.g., stop-loss orders)
2. Explore machine learning approaches for dynamic parameter optimization
3. Extend the strategy to multiple pairs or a basket of stocks
4. Incorporate fundamental data for more robust pair selection
5. Implement real-time trading capabilities

## License

Distributed under the MIT License. See `LICENSE` for more information.
