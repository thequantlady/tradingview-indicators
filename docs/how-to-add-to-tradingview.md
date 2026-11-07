# How to add the indicators to TradingView

No coding needed. Takes about 2 minutes per indicator. Works on the free plan.

## 1. Copy the code from GitHub

1. Open the indicator file in this repository:
   - [`indicators/QuantLady_GoldenCross.pine`](../indicators/QuantLady_GoldenCross.pine)
   - [`indicators/QuantLady_ROC.pine`](../indicators/QuantLady_ROC.pine)
2. Click the **Copy raw file** button (two overlapping squares) at the top-right of the code box.

## 2. Paste it into TradingView

1. Go to [tradingview.com](https://www.tradingview.com), sign in, and open any chart (for example NIFTY).
2. At the bottom of the screen, click **Pine Editor**.
3. Press **Ctrl + A** (Mac: **Cmd + A**) and **Delete** to clear the editor.
4. Paste the code with **Ctrl + V** (Mac: **Cmd + V**).
5. Click **Save** and type a name, for example `QL Golden Cross`.
6. Click **Add to chart**.

It now appears in **Indicators → My scripts**, so next time you can add it with one click.

## 3. Settings

### Golden Cross (`QL Golden Cross`)

Click the indicator name on the chart → ⚙ **Settings**.

| Setting | Use it like this |
|---|---|
| **Preset → Daily · Ep 1** | Chart on **1D**. 50-day and 200-day averages, as in Episodes 1 and 2 |
| **Preset → Weekly · Ep 3** | Chart on **1W**. 10-week and 40-week averages, as in Episode 3 |
| **Preset → Custom** | Your own lengths in the "Custom values" group |
| **Apply channel filters** | On = only crosses that pass volume, near-52-week-high, liquidity and price filters get a green **GC**. Off = every cross |
| **Show crosses that failed the filters** | Grey dots for crosses that were filtered out |

Marks on the chart: gold line = fast average, blue line = slow average, green ▲ **GC** = golden cross, red ▼ **DC** = death cross (the exit used in the episodes).

> Index charts such as NIFTY have no volume data on TradingView, so the volume filter fails there. Turn **Apply channel filters** off when viewing an index.

### ROC % (`QL ROC %`)

| Setting | Default | Meaning |
|---|---|---|
| ROC length | 18 | Compare today's close with the close 18 periods ago |
| Measure on timeframe | 1M | Monthly closes, as in Episode 2. Leave empty for the chart's timeframe |
| Upper / lower reference | 40% / 0% | The two lines discussed in Episode 2 |

The newest value moves until the month closes. The episode uses month-end values only.

## Troubleshooting

| Problem | Fix |
|---|---|
| Red error at the bottom of Pine Editor | You probably copied only part of the code. Clear the editor and copy the full raw file again |
| "Preset is Daily · switch chart to 1D" label | Change the chart timeframe to match the preset |
| Can't add a third indicator | The free plan allows 2 per chart. Remove one, or use a second chart tab |
