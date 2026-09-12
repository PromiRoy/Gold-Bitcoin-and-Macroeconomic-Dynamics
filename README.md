# Gold, Bitcoin, and Macroeconomic Dynamics

**Is gold a hedge, a safe haven, or neither? Is Bitcoin "digital gold"?**
An econometric study of gold, Bitcoin, and U.S. macro-financial variables from
January 2008 to August 2025 — a sample spanning the Global Financial Crisis,
COVID-19, the 2022–23 inflation shock, and the rise of digital assets.

📄 [Thesis (PDF, 68 pp.)](thesis_gold_bitcoin_macro_dynamics.pdf) ·
🧪 [R analysis — full code and output (PDF)](analysis_r_markdown_output.pdf) ·
📊 [Dataset (CSV)](Gold_Data_Final.csv)

## Headline findings

| Question | Method | Result |
|---|---|---|
| Can gold's own history forecast its price? | ARIMA on daily prices, 60-day hold-out | **No, beyond one day.** Best model is ARIMA(0,1,0) — a random walk. Rolling one-step RMSE $29.19 (MAPE 0.67%); the 60-day fixed-origin forecast is just a flat line at the last price. |
| Which macro factors drive gold? | Monthly VECM (gold, USD index, S&P 500, CPI, 10-yr Treasury, unemployment); FEVD, IRFs, Granger tests | **Unemployment, not inflation.** At 12 months unemployment explains 33.6% of gold's forecast-error variance vs. 7.4% for CPI — and the CPI response is *negative*, the opposite of a textbook inflation hedge. The unemployment share is 2020-driven (≈10% excluding the pandemic), so the reliable result is the *ranking and sign*, not the size. |
| Does Bitcoin behave like gold? | 30-day rolling volatility, GARCH(1,1), DCC-GARCH, annual and VIX-regime correlations (2014–2025) | **No.** Bitcoin's annualized volatility averages 62% vs. 14% for gold. Its correlation with the S&P 500 flips positive from 2020 on (+0.43 to +0.56) and jumps from +0.07 on calm days to +0.39 on high-VIX days (+0.49 in the top decile). Gold stays near zero (mean DCC correlation −0.02, negative on 57% of days). |

**Bottom line:** gold acts as a *conditional* hedge against economic
deterioration — steady, near-uncorrelated with equities, but not strictly
protective on the very worst days. Bitcoin behaves as a speculative risk asset,
and the gap between the two has widened since 2020.

## Data

Eleven daily/monthly series, 4,443 trading days (2008-01-02 → 2025-08-29),
all from public sources so the dataset is fully reconstructible:

| Series | Source | Freq. |
|---|---|---|
| Gold (XAU/USD), silver, WTI crude, S&P 500, USD Index (DXY), Bitcoin (from 2014-09-17) | Yahoo Finance | Daily |
| Federal funds rate, 10-yr Treasury yield, CPI, unemployment rate | FRED (St. Louis Fed) | Monthly |
| CBOE VIX (`VIXCLS`) | FRED | Daily |

`Gold_Data_Final.csv` is the cleaned file used in the analysis (74 stale
weekend/holiday placeholder rows removed; the script asserts this on load).
Silver, crude oil, and the funds rate are included for context only; the models
use gold, DXY, S&P 500, CPI, the 10-yr yield, unemployment, and the VIX.

## Methods

1. **Stationarity & forecasting** — ADF/KPSS tests, `auto.arima`, fixed-origin
   vs. rolling one-step-ahead evaluation (RMSE, MAE, MAPE).
2. **Long-run macro linkages** — Johansen cointegration at monthly frequency
   (matching the release schedule of the macro series), VECM with rank r = 2,
   Cholesky-identified FEVD and impulse responses, Toda–Yamamoto Granger
   causality, and sub-sample robustness (with/without 2020; r = 1).
3. **Volatility & dependence** — GARCH(1,1) per asset with residual
   diagnostics, DCC-GARCH dynamic correlations, year-by-year correlations, and
   a stress-regime split on the official CBOE VIX (75th and 90th percentiles).

Implemented in **R**: `forecast`, `tseries`, `urca`, `vars`, `tsDyn`,
`rugarch`, `rmgarch`, `lmtest`, `aod`, `ggplot2`. The complete, annotated
R Markdown — every model, table, and figure — is in
[`analysis_r_markdown_output.pdf`](analysis_r_markdown_output.pdf).

## Reproducing

```r
install.packages(c("forecast","tseries","urca","vars","tsDyn","rugarch",
                   "rmgarch","lmtest","FinTS","aod","car","zoo","ggplot2",
                   "reshape2","corrplot","dplyr","knitr","scales"))
```

Point `raw_path` at `Gold_Data_Final.csv` and knit the R Markdown. The source
`.Rmd` will be added to this repository; until then the knitted PDF contains
the full code.

## Limitations

U.S.-centric variables and stress measure; a six-variable VECM to preserve
degrees of freedom; Bitcoin's post-2020 regime rests on a short history;
GARCH models capture conditional volatility but not all tail risk. See
Chapter 7.4 of the thesis.

## Author

Promi Roy — [LinkedIn](https://www.linkedin.com/in/promiroy)
