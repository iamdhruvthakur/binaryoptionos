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

## MARKET BEHAVIOR

```dataview
TABLE WITHOUT ID
  market-behavior as "Behavior",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => r.stake)) / max(length(rows), 1), 2) as "Avg Stake",
  round(sum(map(rows, (r) => r.payout)) / max(length(rows), 1), 1) + "%" as "Avg Payout",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY market-behavior
SORT length(rows) DESC
```

> *No market behavior data. Behavior is classified when creating a binary trade: NORMAL, REVERSAL, or UNKNOWN.*

---

## DIRECTION

### CALL vs PUT

```dataview
TABLE WITHOUT ID
  direction as "Direction",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY direction
SORT length(rows) DESC
```

> *No directional data available.*

---

## EXPIRY

```dataview
TABLE WITHOUT ID
  expiry as "Expiry",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY expiry
SORT length(rows) DESC
```

> *No expiry performance data.*

---

## PAYOUT ANALYSIS

```dataview
TABLE WITHOUT ID
  payout + "%" as "Payout Level",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY payout
SORT payout DESC
```

> *No payout distribution data.*

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
TABLE date, time, asset, direction, result, strategy-version as "Version"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
SORT date DESC, time DESC
LIMIT 15
```

> *No trades recorded yet.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Trading|Trading]] · [[_Bases/Trades.base|Trades Database]]*
