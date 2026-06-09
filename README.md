# Quantitative Trading Strategy Risk Analysis & Stress Testing

## Overview

This project provides a comprehensive framework for evaluating the robustness and risk characteristics of algorithmic trading strategies. The analysis extends beyond traditional performance metrics by incorporating Value at Risk (VaR), drawdown analysis, slippage stress testing, and Monte Carlo simulations.

The objective is to assess whether a trading strategy remains profitable and resilient under realistic market conditions and execution constraints.

---

## Features

### Performance Metrics

- Compound Annual Growth Rate (CAGR)
- Sharpe Ratio
- Trade-by-Trade Volatility
- Annualized Weekly Volatility
- Annualized Monthly Volatility
- Annualized Quarterly Volatility
- Annualized Yearly Volatility

### Risk Analysis

- Historical Value at Risk (95% Confidence Level)
- Return Distribution Analysis
- Maximum Drawdown Calculation
- Drawdown Visualization

### Slippage Stress Testing

- Simulates increasing transaction costs
- Generates stressed equity curves
- Evaluates profitability degradation
- Compares CAGR across multiple slippage scenarios

### Monte Carlo Simulation

- Simulates future equity paths using historical return statistics
- Generates hundreds of possible outcomes
- Estimates strategy robustness and downside risk

---

## Project Workflow

### 1. Historical Return Analysis

Weekly returns are calculated from the strategy equity curve.

```python
weekly_returns = equity_curve.resample("W").last().pct_change()
```

The return distribution is then used to estimate Value at Risk (VaR).

---

### 2. Value at Risk (VaR)

Historical VaR is estimated using the 5th percentile of weekly returns.

```python
var_95 = weekly_returns.quantile(0.05)
```

#### Interpretation

If:

```text
VaR(95%) = -5%
```

Then:

> There is a 5% probability that the portfolio may lose more than 5% in a given week based on historical observations.

---

### 3. Volatility Analysis

The framework calculates volatility at multiple frequencies:

- Trade-by-Trade
- Weekly
- Monthly
- Quarterly
- Yearly

Annualization is performed using the square-root-of-time rule.

---

### 4. Maximum Drawdown

Maximum Drawdown measures the largest peak-to-trough decline in portfolio value.

```python
drawdown = (equity_curve - equity_curve.cummax()) / equity_curve.cummax()
```

This provides insight into the worst historical loss experienced by the strategy.

---

### 5. Slippage Stress Testing

Transaction costs are artificially increased to evaluate strategy resilience.

```python
Stressed_PnL = PnL - TransactionValue * SlippageRate
```

The framework:

- Recalculates equity curves
- Generates multiple stress scenarios
- Measures CAGR deterioration
- Identifies profitability breakpoints

---

### 6. Monte Carlo Simulation

Future returns are simulated using a normal distribution parameterized by historical returns.

```python
simulated_returns = np.random.normal(mean, std, n_days)
```

The simulation helps evaluate:

- Potential future growth paths
- Variability of outcomes
- Downside scenarios
- Long-term strategy robustness

---

## Visualizations

The project automatically generates the following charts:

### Return Distribution

- Histogram of weekly returns
- 95% VaR threshold
- Highlighted loss region

### Drawdown Curve

- Portfolio drawdown over time
- Maximum drawdown marker

### Slippage Stress Test

- Multiple stressed equity curves
- Comparison against actual equity curve

### CAGR Under Different Slippage Scenarios

- Bar chart of CAGR degradation
- Sensitivity analysis

### Monte Carlo Simulations

- Hundreds of projected equity paths
- Average expected trajectory

---

## Input Data Structure

The input file should contain the following columns:

| Column | Description |
|----------|------------|
| Exit_date | Trade exit date |
| Price | Entry price |
| Exit_Price | Exit price |
| Qty | Quantity traded |
| PnL | Profit/Loss per trade |
| equity_curve | Running portfolio value |

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- SciPy

---

## Applications

This framework is suitable for:

- Quantitative Trading Research
- Algorithmic Trading Validation
- Portfolio Risk Management
- Backtesting Analysis
- Execution Cost Analysis
- Hedge Fund Research
- Strategy Robustness Testing

---

## Future Improvements

Potential extensions include:

- Conditional Value at Risk (CVaR)
- Bootstrap Monte Carlo Simulation
- Regime-Based Stress Testing
- Walk-Forward Analysis
- Portfolio Optimization
- Risk Attribution Analysis
- Transaction Cost Modelling
- Probabilistic Sharpe Ratio

---

## Key Objective

The purpose of this project is to evaluate whether a trading strategy can survive realistic market conditions rather than simply produce attractive backtest returns. By combining historical risk measures, slippage stress testing, and Monte Carlo simulations, the framework provides a more complete assessment of strategy robustness and risk-adjusted performance.
