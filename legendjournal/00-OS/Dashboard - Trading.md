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

<div class="tos-subtitle">Quotex Performance Analytics</div>

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

## CORE PERFORMANCE

### All Time

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  length(filter(rows, (r) => r.result = "VOID")) as "V",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => r.stake)) / max(length(rows), 1), 2) as "Avg Stake",
  round(sum(map(rows, (r) => r.payout)) / max(length(rows), 1), 1) + "%" as "Avg Payout",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY true
```

> *No trades recorded yet.*

### Today

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND date = date(today)
GROUP BY true
```

### Last 7 Days

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND date >= date(today) - dur(7 days)
GROUP BY true
```

---

## QUOTEX TRADE ANALYSIS

### By Asset

```dataview
TABLE WITHOUT ID
  asset as "Asset",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY asset
SORT length(rows) DESC
```

### By Direction (CALL vs PUT)

```dataview
TABLE WITHOUT ID
  direction as "Direction",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY direction
SORT length(rows) DESC
```

### By Expiry

```dataview
TABLE WITHOUT ID
  expiry as "Expiry",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY expiry
SORT length(rows) DESC
```

### By Payout Level

```dataview
TABLE WITHOUT ID
  payout + "%" as "Payout Level",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY payout
SORT payout DESC
```

### By OTC Market Behavior

```dataview
TABLE WITHOUT ID
  market-behavior as "Behavior",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY market-behavior
SORT length(rows) DESC
```

### By Strategy Version

```dataview
TABLE WITHOUT ID
  strategy-version as "Version",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY strategy-version
SORT length(rows) DESC
```

---

## TRADE QUALITY & FEEDBACK

```dataview
TABLE mistake as "Mistake", psychology-flag as "Psych Flag", evidence as "Evidence"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND (mistake != "" OR psychology-flag = true OR length(evidence) > 0)
SORT date DESC
LIMIT 10
```

> *No recent trades with quality flags or evidence attached.*

---

## ALL TRADES LOG

> Open [[_Bases/Trades.base|Trades Database]] for the full filterable view.

```dataview
TABLE date, time, asset, direction, expiry, result, stake, payout + "%" as "Payout", round(choice(result = "WIN", stake * (payout/100), choice(result = "LOSS", -stake, 0)), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
SORT date DESC, time DESC
LIMIT 25
```

---
*[[Dashboard - Trading OS|Home]] · [[_Bases/Trades.base|Trades Database]]*
