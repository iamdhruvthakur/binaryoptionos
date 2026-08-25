<%*
const date = tp.date.now("YYYY-MM-DD");
const dateCompact = tp.date.now("YYYYMMDD");
const unique = Math.random().toString(36).substring(2, 6).toUpperCase();
const seq = tp.date.now("HHmmss") + "-" + unique;
const fileName = "BT-" + dateCompact + "-" + seq;
const assets = ["EUR-USD", "GBP-USD", "USD-JPY", "AUD-USD", "EUR-GBP"];
const asset = await tp.system.suggester(assets, assets, false, "Asset:") ?? "UNSET";
const regimes = ["Normal", "Reversal", "Choppy", "Trending"];
const regime = await tp.system.suggester(regimes, regimes, false, "Market Regime:") ?? "UNSET";
await tp.file.rename(fileName);
await tp.file.move("03-Research/Backtests/" + fileName);
-%>
---
note-type: backtest
id: <% fileName %>
date-run: <% date %>
strategy: "[[STR-V6]]"
strategy-version: ""
asset: "[[AST-<% asset %>]]"
session: ""
market-regime: "[[REG-<% regime %>]]"
date-range-start: ""
date-range-end: ""
total-trades: 0
wins: 0
losses: 0
voids: 0
win-rate: 0
notes: ""
conclusion: ""
evidence: []
tags:
  - backtest
---

# Backtest: <% fileName %>

> **Asset:** <% asset %> | **Regime:** <% regime %> | **Run:** <% date %>

## Backtest Parameters

| Parameter | Value |
|---|---|
| Strategy Version | |
| Asset | <% asset %> |
| Session | |
| Market Regime | <% regime %> |
| Date Range | -- |
| Sample Size | |

## Results

| Metric | Value |
|---|---|
| Total Trades | |
| Wins | |
| Losses | |
| Voids | |
| Win Rate | % |

## Trade Log

| # | Date | Time | Direction | Result | Notes |
|---|---|---|---|---|---|
| 1 | | | | | |

## Analysis

## Conclusion

## Evidence / Screenshots

---
*[[Dashboard - Research|Research Dashboard]]* | *[[Dashboard - Trading OS|Home]]*