# Gold, Bitcoin, and Macroeconomic Dynamics

Econometric analysis of whether macroeconomic factors carry
predictive signal for gold and Bitcoin, January 2008 to August 2025.

## Summary

This project examines the behaviour of gold, Bitcoin, and a set of
macroeconomic and financial variables between January 2008 and
August 2025. It asks three questions. Can gold prices be predicted
from their own history? Which macroeconomic factors explain gold's
movements? Does Bitcoin behave as a hedge, a safe haven, or a
speculative asset?

An ARIMA model tests whether past gold prices forecast future ones.
A Vector Error Correction Model, estimated at monthly frequency,
relates gold to CPI, unemployment, the 10-year Treasury yield, the
U.S. Dollar Index, and the S&P 500. GARCH(1,1) and DCC-GARCH models
with VIX regime splits compare volatility and equity correlation
across calm and high-stress periods.

Gold follows a random walk in the short run. At twelve months,
unemployment accounts for about 33.6% of gold's forecast error
variance against 7.4% for CPI, with opposite signs; the share is
2020-driven, so the finding is the ranking and direction, not the
size. Bitcoin runs at roughly four times gold's volatility and has
moved increasingly with equities since 2020.

## Full write-up

[Macroeconomic Data Analysis (PDF)](Macroeconomic_Data_Analysis.pdf) 
[Gold and Bitcoin analysis (PDF)](Gold_pdf.pdf)

## Data

Prices from Yahoo Finance, macro series from FRED. Public sources;
retrieval scripts included.
