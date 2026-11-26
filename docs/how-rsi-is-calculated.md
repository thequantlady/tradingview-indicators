# How RSI is calculated (plain words, with numbers you can check)

RSI (Relative Strength Index) was introduced by J. Welles Wilder in 1978. The standard setting is **14**. This page explains exactly what it measures, using small examples you can check with a calculator.

The channel uses the same method as TradingView's built-in `ta.rsi()`, so every RSI value in our videos and result files should match what you see on your own chart.

---

## 1. The idea in one line

> **RSI compares how big the recent up-moves were with how big the recent down-moves were. The newest days count a little more.**

- RSI goes from 0 to 100.
- Above 50: the recent up-moves were bigger than the down-moves.
- Below 50: the recent down-moves were bigger.
- RSI 70 means about 70% of the recent movement was up-moves, which is roughly 2.3 times the down-moves.
- RSI 30 means about 70% of the recent movement was down-moves.

Whether 70 means "overbought" (about to fall) is a separate claim. That is what our RSI episodes test with data.

---

## 2. It measures size, not the number of days

RSI does **not** count up days and down days. It adds up **how far** the price moved, in rupees.

Example over 4 days, stock starting at ₹100:

| Day | Move |
|---|---|
| 1 | up ₹1 |
| 2 | up ₹1 |
| 3 | up ₹1 |
| 4 | down ₹9 |

Three days up, one day down. But:

- total up-moves = ₹3
- total down-moves = ₹9
- simple RSI = 100 × 3 ÷ (3 + 9) = **25**

So a stretch with mostly up days can still have a low RSI, if the few down days were big.

---

## 3. The exact formula, step by step

**Step 1: each day's move.** Change = today's close − yesterday's close.

- If the change is positive, it is today's **up-move** (and today's down-move is 0).
- If the change is negative, its size is today's **down-move** (and today's up-move is 0).

**Step 2: the first average (day 14).** Take the plain average of the first 14 up-moves and the first 14 down-moves. Days with no up-move count as 0 in the up average, and the same for down.

**Step 3: every day after that (Wilder's smoothing).**

```
new average up   = (13 × yesterday's average up   + today's up-move)   ÷ 14
new average down = (13 × yesterday's average down + today's down-move) ÷ 14
```

"Yesterday's average up" is simply the number you calculated the day before. Each day you keep 13 parts of it and add today's move as the 14th part.

**Step 4: RSI.**

```
RSI = 100 × average up ÷ (average up + average down)
```

This is the same as Wilder's original form, `RSI = 100 − 100 ÷ (1 + RS)` with `RS = average up ÷ average down`.

---

## 4. Worked example (you can check every number)

Closing prices for 17 days:

`100, 104, 102, 105, 102, 107, 106, 108, 104, 110, 108, 112, 111, 115, 114, 119, 113`

**Day 14** (after the first 14 moves):

- the up-moves add up to ₹28, so average up = 28 ÷ 14 = **₹2.00**
- the down-moves add up to ₹14, so average down = 14 ÷ 14 = **₹1.00**
- RSI = 100 × 2.00 ÷ (2.00 + 1.00) = **66.67**

**Day 15: price goes up ₹5** (114 to 119)

- average up = (13 × 2.00 + 5) ÷ 14 = **₹2.2143**
- average down = (13 × 1.00 + 0) ÷ 14 = **₹0.9286**
- RSI = 100 × 2.2143 ÷ (2.2143 + 0.9286) = **70.45**

**Day 16: price goes down ₹6** (119 to 113)

- average up = (13 × 2.2143 + 0) ÷ 14 = **₹2.0561**
- average down = (13 × 0.9286 + 6) ÷ 14 = **₹1.2908**
- RSI = 100 × 2.0561 ÷ (2.0561 + 1.2908) = **61.43**

Run these 17 prices through the Python code in section 8, or a spreadsheet, and you will get 66.67, 70.45 and 61.43.

---

## 5. Why the newest days count more

Because the old average is multiplied by 13/14 every day, each day's move fades a little every day after it happens:

| Move from | Share of today's average |
|---|---|
| today | 7.14% |
| yesterday | 6.63% |
| 2 days ago | 6.16% |
| 13 days ago | 2.73% |
| **all 14 most recent days together** | **about 65%** |
| everything older than 14 days | about 35% |

So "RSI 14" does **not** mean "only the last 14 days". It means all past days, with the most recent ones counting the most. That is also why RSI values can differ slightly between websites that start their data on different dates.

---

## 6. The order of the moves matters

Two stretches with the same moves in a different order give different RSI values.

Test: a stock that has been moving sideways (RSI about 52), followed by 14 days with 4 down days totalling −16% and 10 up days totalling +7%. Net move about −10% in both cases.

| Order | RSI at the end (TradingView method) | Plain 14-day ratio |
|---|---|---|
| fall first, then the small rises | 42.8 | 26.9 |
| small rises first, then the fall | 26.5 | 29.0 |

- When the fall is the most recent thing, RSI ends lower, because recent days count more.
- Neither order gets anywhere near 70, because the down-moves were much bigger than the up-moves.
- Even the plain ratio changes a little with order, because the same percentage move is a different rupee amount at a different price.

---

## 7. Simplified version in our videos

To explain the idea on screen, the videos sometimes show the **plain 14-day ratio** (total up ÷ total up and down). It is labelled "simplified". Every backtest number uses the full formula in section 3.

---

## 8. The code

**TradingView (Pine Script):**

```pine
r = ta.rsi(close, 14)
```

**Python (same method as the channel's backtests):**

```python
import numpy as np, pandas as pd

def rsi_wilder(close: pd.Series, n: int = 14) -> pd.Series:
    d = close.diff()
    up, dn = d.clip(lower=0), -d.clip(upper=0)
    a = np.full(len(close), np.nan); b = np.full(len(close), np.nan)
    a[n] = up.iloc[1:n+1].mean(); b[n] = dn.iloc[1:n+1].mean()      # step 2: plain average
    for i in range(n + 1, len(close)):                                # step 3: Wilder's smoothing
        a[i] = (a[i-1] * (n - 1) + up.iloc[i]) / n
        b[i] = (b[i-1] * (n - 1) + dn.iloc[i]) / n
    return pd.Series(100 * a / (a + b), index=close.index)           # step 4

prices = pd.Series([100,104,102,105,102,107,106,108,104,110,108,112,111,115,114,119,113], dtype=float)
print(rsi_wilder(prices).round(2).tolist()[14:])   # [66.67, 70.45, 61.43]
```

---

*Education only. Not investment advice, not a stock tip. See [DISCLAIMER.md](../DISCLAIMER.md).*
