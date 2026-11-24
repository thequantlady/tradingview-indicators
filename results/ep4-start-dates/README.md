# Episode 4 — 30 Months. Zero Trades. Does the Start Date Matter?

Same strategy as Episode 3 (weekly Golden Cross + cycle filter), same ₹10 lakh, same costs and tax rules.
Idle cash earns 6% a year, as in Episode 3. The only thing that changes is **the date you start**.

## Test 1 — 121 start dates, all held to December 2025

A new portfolio was started on the first trading day of every month from January 2013 to January 2023 (121 portfolios) and held to December 2025.

| Result | Value |
|---|---|
| Portfolios that beat the Nifty 50 (price index), after tax | 121 of 121 |
| Average CAGR after tax | 28.8% |
| January 2013 (the start used in Episodes 1–3) | rank 83 of 121 by CAGR after tax — below average |
| Share of profit from the top 3 trades (median run) | about 51% |

These are **not 121 independent proofs**. The portfolios overlap in time and most of them hold the same big trades (89 of 121 held the same two June 2020 trades).

## Test 2 — 96 fair windows, each held exactly 5 years

Start every month from January 2013 to December 2020 and hold exactly 5 years (the last window ends December 2025).

| Window | Value of ₹10 lakh after costs |
|---|---|
| Worst (Apr 2015 → Apr 2020, ended in the Covid crash) | ₹16.0 lakh |
| Middle (median) | ₹46.8 lakh |
| Best (May 2020 → May 2025, started at the Covid bottom) | ₹91.3 lakh |
| Windows that lost money | 0 of 96 |

## Files

| File | What it contains |
|---|---|
| [`start_dates_121.csv`](start_dates_121.csv) | One row per start month: final value after costs and after tax (₹ lakh), CAGR, Nifty 50 price CAGR over the same dates, max drawdown, number of trades, first entry date, win rate, share of profit from the top 3 trades |
| [`windows_5y_96.csv`](windows_5y_96.csv) | One row per 5-year window: start and end month, value after costs and after tax, Nifty 50 price value, max drawdown, % of days in cash |

## Notes

- Nifty comparison uses the **price index** (no dividends). Dividends add roughly 1–1.5% a year; the smallest gap between the strategy and the Nifty was still about 5 percentage points a year.
- The cycle filter sent the strategy to cash only 4 times in 13 years. Four events cannot validate a rule.
- Data: Yahoo Finance daily prices for NSE stocks, cleaned as described in Episode 1. Survivorship bias is not fully removed.
- Backtested, hypothetical results. Past performance does not predict future returns. Education only — see [DISCLAIMER](../../DISCLAIMER.md).

## Episode links

- Watch Episode 4: [YouTube channel](https://www.youtube.com/@theQuantLady)
- Trade-by-trade detail for the January 2013 start: [Episode 3 results](../ep3-weekly-golden-cross/README.md)
