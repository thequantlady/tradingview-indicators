# How the code works (plain words)

Pine Script is TradingView's language for indicators. Each script runs once on every bar (candle) of the chart, from the oldest to the newest.

## Golden Cross script, part by part

| Code | In plain words |
|---|---|
| `//@version=6` | Use Pine Script version 6 |
| `indicator("…", overlay = true)` | Name the indicator and draw it on top of the price chart |
| `input.string(...)`, `input.int(...)` | Settings the viewer can change in the ⚙ menu |
| `fast = ta.sma(close, fastLen)` | Fast average: the average closing price of the last 50 bars |
| `slow = ta.sma(close, slowLen)` | Slow average: the last 200 bars |
| `ta.crossover(fast, slow)` | True on the bar where the fast average moves above the slow one: a **golden cross** |
| `ta.crossunder(fast, slow)` | True where it moves below: a **death cross** |
| `volume > 1.2 * ta.sma(volume, 20)` | Volume is at least 20% above its 20-day average |
| `close >= 0.70 * ta.highest(high, 250)` | Price is within 30% of its 52-week high |
| `ta.median(close * volume, 50) >= 50 lakh` | Typical daily trading value is at least ₹50 lakh (liquid enough) |
| `ta.median(close, 50) >= 20` | Typical price is at least ₹20 |
| `plot(...)` | Draw the two average lines |
| `plotshape(...)` | Draw the ▲ GC and ▼ DC marks |

## ROC % script

`ta.roc(close, 18)` = (today's close ÷ the close 18 periods ago − 1) × 100.
`request.security(..., "1M", ...)` asks TradingView for the same calculation on **monthly** closes, even if your chart shows daily candles.
`hline(40)` and `hline(0)` draw the two reference lines.

## Try changing it yourself

1. Open the script in **Pine Editor**.
2. Change a number, for example the volume multiplier `1.2` to `1.5`.
3. Click **Save**. The chart updates instantly.

That is how every "what if" test starts. But remember Episode 3: a better-looking past is not a better future.
