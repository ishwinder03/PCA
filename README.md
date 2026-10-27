# SOFR Swap Curve PCA: Rich / Cheap

| Notebook | What it is |
|---|---|
| **`pca_fly_analysis.ipynb`** | Trader-facing PCA rich/cheap on SOFR **flies**: point-in-time residuals, fly z-scores, backtest (ex costs), IS/OOS, live `score_today()` snapshot, short-history mode |
| **`regime_pca_fair_value.ipynb`** | Plain vs regime-matched PCA fair value for SOFR flies: matched historical 3M windows, latest-day rich/cheap table, matching diagnostics, 10-day reversal check (no P&L) |
| `sofr_swap_pca.ipynb` | First version: per-tenor residuals, PC1/PC2-hedged flies with costs |

Both read the simulated levels in `sofr_swap_rates_simulated.csv`.

### `sofr_swap_pca.ipynb`

1. Simulated SOFR swap curve (3y–15y, 20y, 25y, 30y), 2016–2025
2. PCA on daily changes: level / slope / curvature
3. Rolling, past-only 3-factor fit, residuals (bp) and z-scores (rich / cheap)
4. Backtest of PC1/PC2-hedged butterflies (enter at ±2σ, exit at 0), net of bid-offer
5. Caveat: a structural break in the 20y

```bash
pip install -r requirements.txt
jupyter notebook sofr_swap_pca.ipynb
```

The simulated daily levels are also saved as **`sofr_swap_rates_simulated.csv`** (date × tenor, rates in %).
The notebook regenerates the same data with a fixed seed.

To use real data, replace the `rates = simulate_sofr_curve()` line in Section 1 with a DataFrame of
rates in percent, indexed by date, with columns `3y … 30y`. Results on simulated data illustrate the
method only.
