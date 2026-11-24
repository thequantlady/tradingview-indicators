# Episode 3 · Weekly Golden Cross: complete backtest results

These are the full results behind **The Quant Lady, Episode 3**: the Golden Cross strategy on a **weekly chart (10/40-week averages)**, with the Episode 2 cycle filter and 6% a year on idle cash.

> **Education only.** This is a historical backtest, not investment advice, not stock tips and not a signal service. Every trade here closed before the end of 2025. Past results do not predict the future. Talk to a SEBI-registered adviser before investing.

## Summary (₹10 lakh start, 1 Jan 2013 to 31 Dec 2025)

| | Result |
|---|---|
| Final value after costs | ₹2.83 crore (29.3% a year) |
| Final value after tax | ₹2.07 crore (26.2% a year) |
| Worst fall (after costs) | −18.9% |
| Trades | 72 (49 winners, 23 losers, 68% win rate) |
| Average winner / average loser | +114% / −13% |
| Trades that at least doubled | 17 |
| Trading costs paid | ₹2.15 lakh |
| Interest earned on idle cash (6%) | ₹38.9 lakh |
| Tax paid | ₹33.6 lakh |

## The rules

- **Universe:** NSE stocks with a median daily turnover of at least ₹50 lakh and a price of at least ₹20.
- **Buy signal:** the 10-week average closes above the 40-week average (weekly golden cross), checked at the Friday close. The same week's volume must be more than 1.2× its 4-week average, and the close must be within 30% of the 52-week high.
- **Buy:** at the next trading day's open. The portfolio has 10 slots, and each buy is one-tenth of the portfolio's current value (₹1 lakh at the start). If all 10 slots are full, no new buys until a stock is sold.
- **Sell:** when the 10-week average closes below the 40-week average (weekly death cross), at the next trading day's open.
- **Cycle filter (from Episode 2):** at every month-end, if the Nifty 50 is 40% or more above where it was 18 months ago, sell everything and stay in cash. Start buying again only after that number falls to zero or below.
- **Idle cash** earns 6% a year, like a liquid fund.
- **Costs:** statutory charges (0.12% on buys, 0.11% on sells) plus 0.15% slippage on every trade. **Tax:** short- and long-term capital gains tax at the rates in force each year, plus interest taxed at the 30% slab (with cess).

## Files

| File | What it contains |
|---|---|
| [`trades.csv`](trades.csv) | All 72 trades: stock, signal week, entry and exit dates and prices, amount invested, profit or loss, return, exit reason, tax type |
| [`yearly_returns.csv`](yearly_returns.csv) | Return for each year: weekly strategy (after costs and after tax), the daily Episode 2 version (after tax) and the Nifty 50 |
| [`equity_monthly.csv`](equity_monthly.csv) | Portfolio value at every month-end (after costs and after tax), the deepest fall from the previous peak reached at any point during that month (`drawdown_pct`, so it can be negative even when the month ended at a new high), and number of stocks held |
| [`settings_grid.csv`](settings_grid.csv) | The 14 nearby settings tested in the video. CAGR after costs ranged from 19.6% to 32.3% (median 26.5%) |

## The honest part

- **A few trades did most of the work.** The 5 best trades made 63% of all the profit. The median trade returned +17%.
- **38 of the 72 trades were closed by the cycle filter**, not by a death cross. Many winners were sold early because the whole market looked too hot.
- **The weekly chart did not give fewer signals.** 6,982 weekly golden crosses against 6,516 daily ones (2013 to 2025).
- **It is not always better than daily.** In 2016, 2023 and 2024 the daily Episode 2 version did better. Across the 14 settings, only 3 beat the daily version (27.3% a year after costs).
- **Long spells in cash.** The strategy was fully in cash in 2015, 2018, 2019, 2022 and 2025, earning only the 6%.

## Notes on the data

- Prices are adjusted for splits and bonuses, so they will not match old newspaper quotes.
- Stocks that were delisted are missing from the data (survivorship bias), which flatters the results.
- After-tax yearly returns depend on when tax is accounted for, so a single year can look slightly higher after tax than after costs (2015). The final value is not affected.
- Nifty 50 returns are price returns, without dividends.
- **Known data issue:** trades 24 and 25 (AKZOINDIA and JSWDULUX) are the same company under its old and new NSE symbols. The price data listed it twice, so this one small losing position was counted twice. The extra loss is about ₹10,600, well under 0.1% of the final value, so the results do not change in any meaningful way. We have left the rows as they were run rather than edit the backtest after the fact.

## Episode links

- Watch Episode 3: [YouTube channel](https://www.youtube.com/@theQuantLady)
- The weekly indicator for TradingView: [`QuantLady_GoldenCross.pine`](../../indicators/QuantLady_GoldenCross.pine), preset **Weekly · Ep 3**
