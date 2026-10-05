# Portfolio Optimization with Walk-Forward Validation

Monte Carlo simulation and scipy-based mean-variance (Markowitz) optimization for a
4-stock portfolio (AAPL, MSFT, Block/XYZ, AMZN), with an out-of-sample walk-forward
backtest to check whether the optimized weights actually hold up on unseen data.

**Key finding:** the scipy-optimized max-Sharpe portfolio showed no real edge over a
naive equal-weight (1/N) portfolio once tested out-of-sample, despite being far more
concentrated. This matches the well-known result that mean-variance optimization is
highly sensitive to estimation error in expected returns ("Markowitz optimization enigma").

## What's in this notebook

1. **Data** — Daily closing prices for AAPL, MSFT, XYZ (Block), and AMZN pulled live via `yfinance`.
2. **Monte Carlo simulation** — Thousands of random portfolio weightings, plotted as a
   risk/return scatter (the efficient frontier) colored by Sharpe ratio.
3. **Scipy optimization** — `scipy.optimize.minimize` (SLSQP) solving for the exact
   max-Sharpe and min-volatility portfolios.
4. **Walk-forward backtest** — An expanding training window, re-optimized and tested
   month by month on data the optimizer never saw, compared against an equal-weight benchmark.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate   # .venv\Scripts\activate on Windows
pip install -r requirements.txt
```

Then open `test.ipynb` in Jupyter or VS Code, select the `.venv` kernel, and run all cells.

## Credits

Built on top of the structure and core methodology from
[areed1192/portfolio-optimization](https://github.com/areed1192/portfolio-optimization)
(Alex Reed, MIT License). The original tutorial's data-fetching and dependency pins were
from 2020 and no longer work on current Python/library versions, so this project rebuilds
the data pipeline on `yfinance`, updates the code for current pandas/numpy/scipy, and adds
the out-of-sample walk-forward backtest, which the original tutorial did not include.