---
note-type: dashboard
title: Binary Options
cssclasses:
  - dashboard
tags:
  - dashboard
  - binary
---

<div class="tos-nav">
  [[Dashboard - Trading OS|HOME]]
  <strong>BINARY</strong>
  [[Dashboard - Trading|TRADING]]
  [[Dashboard - Strategy|STRATEGY]]
  [[Dashboard - Research|RESEARCH]]
  [[Dashboard - Market|MARKET]]
  [[Dashboard - Psychology|PSYCHOLOGY]]
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# BINARY OPTIONS

<div class="tos-subtitle">Quotex · OTC Market · Algorithmic Behavior Analysis</div>

<div class="quick-actions">

```meta-bind-button
style: primary
label: "+ NEW BINARY TRADE"
id: btn-trade-otc
actions:
  - type: command
    command: quickadd:choice:01-new-trade
```

```meta-bind-button
style: default
label: "+ SESSION"
id: btn-bo-session
actions:
  - type: command
    command: quickadd:choice:02-new-session
```

```meta-bind-button
style: default
label: "+ DAILY REVIEW"
id: btn-bo-review
actions:
  - type: command
    command: quickadd:choice:03-daily-review
```

```meta-bind-button
style: default
label: "+ RESEARCH"
id: btn-bo-research
actions:
  - type: command
    command: quickadd:choice:08-new-research
```

```meta-bind-button
style: default
label: "+ OBSERVATION"
id: btn-bo-obs
actions:
  - type: command
    command: quickadd:choice:10-new-observation
```

</div>

---

## ACCOUNT PERFORMANCE

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "Wins",
  length(filter(rows, (r) => r.result = "LOSS")) as "Losses",
  length(filter(rows, (r) => r.result = "VOID")) as "Voids",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => r.stake)) / max(length(rows), 1), 2) as "Avg Stake",
  round(sum(map(rows, (r) => r.payout)) / max(length(rows), 1), 1) + "%" as "Avg Payout",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type = "BINARY"
GROUP BY true
```

> *No binary trades recorded. Create your first using **+ NEW BINARY TRADE**.*

### Today

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "P/L Today"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type = "BINARY" AND date = date(today)
GROUP BY true
```

### Last 7 Days

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "P/L (7d)"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type = "BINARY" AND date >= date(today) - dur(7 days)
GROUP BY true
```

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
WHERE note-type = "trade" AND trade-type = "BINARY"
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
WHERE note-type = "trade" AND trade-type = "BINARY"
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
WHERE note-type = "trade" AND trade-type = "BINARY"
GROUP BY expiry
SORT length(rows) DESC
```

> *No expiry performance data.*

---

## ASSET PERFORMANCE

```dataview
TABLE WITHOUT ID
  asset as "Asset",
  length(rows) as "Trades",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type = "BINARY"
GROUP BY asset
SORT length(rows) DESC
```

> *No OTC asset performance data.*

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
WHERE note-type = "trade" AND trade-type = "BINARY"
GROUP BY payout
SORT payout DESC
```

> *No payout distribution data.*

---

## RECENT BINARY TRADES

```dataview
TABLE date, time, asset, direction, market-behavior as "Behavior", expiry, result, stake, payout + "%" as "Payout", round(choice(result = "WIN", stake * (payout/100), choice(result = "LOSS", -stake, 0)), 2) as "P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type = "BINARY"
SORT date DESC, time DESC
LIMIT 15
```

> *No binary trades recorded yet.*

---

## ATTENTION

### Unreviewed Binary Sessions

```dataview
TABLE date, session-type, total-trades, win-rate
FROM "01-Journal/Sessions"
WHERE note-type = "session" AND reviewed = false AND contains(session-type, "OTC")
SORT date DESC
LIMIT 5
```

> *All binary sessions reviewed.*

### Binary Mistakes

```dataview
TABLE date, asset, direction, result, mistake
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type = "BINARY" AND mistake AND mistake != ""
SORT date DESC
LIMIT 5
```

> *No mistakes flagged on binary trades.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Trading|Trading]] · [[_Bases/Trades.base|Trades Database]]*
