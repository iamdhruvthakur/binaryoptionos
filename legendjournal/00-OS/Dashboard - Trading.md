---
note-type: dashboard
title: Trading Dashboard
cssclasses:
  - dashboard
tags:
  - dashboard
---

<div class="tos-nav">
  [[Dashboard - Trading OS|HOME]]
  [[Dashboard - Binary Options|BINARY]]
  <strong>TRADING</strong>
  [[Dashboard - Strategy|STRATEGY]]
  [[Dashboard - Research|RESEARCH]]
  [[Dashboard - Market|MARKET]]
  [[Dashboard - Psychology|PSYCHOLOGY]]
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# TRADING

<div class="tos-subtitle">Performance Analytics · All Markets</div>

<div class="quick-actions">

```meta-bind-button
style: primary
label: "+ NEW TRADE"
id: btn-trade
actions:
  - type: command
    command: quickadd:choice:01-new-trade
```

```meta-bind-button
style: default
label: "+ SESSION"
id: btn-session
actions:
  - type: command
    command: quickadd:choice:02-new-session
```

</div>

---

## ALL-TIME PERFORMANCE

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  length(filter(rows, (r) => r.result = "VOID")) as "V",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY true
```

> *No trades recorded yet.*

### Last 7 Days

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND date >= date(today) - dur(7 days)
GROUP BY true
```

### Last 30 Days

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND date >= date(today) - dur(30 days)
GROUP BY true
```

---

## PERFORMANCE BY TRADE TYPE

```dataview
TABLE WITHOUT ID
  trade-type as "Type",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY trade-type
SORT length(rows) DESC
```

> *No trade type data. Trades are classified as FOREX or BINARY.*

---

## PERFORMANCE BY MARKET REGIME

```dataview
TABLE WITHOUT ID
  market-regime as "Regime",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY market-regime
SORT length(rows) DESC
```

> *No regime data available.*

---

## PERFORMANCE BY ASSET

```dataview
TABLE WITHOUT ID
  asset as "Asset",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY asset
SORT length(rows) DESC
```

> *No asset data available.*

---

## PERFORMANCE BY DAY OF WEEK

```dataview
TABLE WITHOUT ID
  day-of-week as "Day",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY day-of-week
SORT length(rows) DESC
```

> *No day-of-week data available.*

---

## PERFORMANCE BY STRATEGY VERSION

```dataview
TABLE WITHOUT ID
  strategy-version as "Version",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY strategy-version
SORT length(rows) DESC
```

> *No version performance data.*

---

## MISTAKE IMPACT

```dataview
TABLE WITHOUT ID
  mistake as "Mistake",
  length(rows) as "Occurrences",
  length(filter(rows, (r) => r.result = "LOSS")) as "Losses",
  round(length(filter(rows, (r) => r.result = "LOSS")) / max(length(rows), 1) * 100, 0) + "%" as "Loss Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND mistake AND mistake != ""
GROUP BY mistake
SORT length(rows) DESC
```

> *No mistakes flagged on trades.*

---

## ALL TRADES

> Open [[_Bases/Trades.base|Trades Database]] for the full filterable view.

```dataview
TABLE date, time, trade-type as "Type", asset, direction, result, strategy-version as "Version"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
SORT date DESC, time DESC
LIMIT 25
```

> *No trades recorded yet.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Binary Options|Binary Options]] · [[_Bases/Trades.base|Trades Database]]*
