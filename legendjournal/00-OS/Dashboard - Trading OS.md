---
note-type: dashboard
title: Trading OS
cssclasses:
  - dashboard
tags:
  - dashboard
  - home
---

<div class="tos-nav">
  <strong>HOME</strong>
  [[Dashboard - Trading|TRADING]]
  [[Dashboard - Strategy|STRATEGY]]
  [[Dashboard - Research|RESEARCH]]
  [[Dashboard - Market|MARKET]]
  [[Dashboard - Psychology|PSYCHOLOGY]]
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# TRADING OS

<div class="tos-subtitle">Binary Options & Forex Research Environment</div>

<div class="tos-status">
  <span><span class="tos-status-dot"></span> <strong>Active</strong></span>
  <span>Strategy: [[STR-V6]]</span>
  <span>Version: [[VER-V6.2]]</span>
</div>

---

## QUICK ACTIONS

<div class="quick-actions">

```meta-bind-button
style: primary
label: "+ NEW TRADE"
id: btn-new-trade
actions:
  - type: command
    command: quickadd:choice:01-new-trade
```

```meta-bind-button
style: default
label: "+ SESSION"
id: btn-new-session
actions:
  - type: command
    command: quickadd:choice:02-new-session
```

```meta-bind-button
style: default
label: "+ DAILY REVIEW"
id: btn-daily-review
actions:
  - type: command
    command: quickadd:choice:03-daily-review
```

```meta-bind-button
style: default
label: "+ WEEKLY REVIEW"
id: btn-weekly-review
actions:
  - type: command
    command: quickadd:choice:04-weekly-review
```

```meta-bind-button
style: default
label: "+ RESEARCH"
id: btn-new-research
actions:
  - type: command
    command: quickadd:choice:08-new-research
```

```meta-bind-button
style: default
label: "+ OBSERVATION"
id: btn-new-observation
actions:
  - type: command
    command: quickadd:choice:10-new-observation
```

</div>

---

## TODAY

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND date = date(today)
GROUP BY true
```

> *No trades today. Use **+ NEW TRADE** to begin.*

```dataview
TABLE time, asset, direction, result
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND date = date(today)
SORT time DESC
```

---

## PERFORMANCE

### All Time

```dataview
TABLE WITHOUT ID
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "Wins",
  length(filter(rows, (r) => r.result = "LOSS")) as "Losses",
  length(filter(rows, (r) => r.result = "VOID")) as "Voids",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY true
```

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

## NEEDS ATTENTION

### Unreviewed Sessions

```dataview
TABLE date, session-type, total-trades, win-rate
FROM "01-Journal/Sessions"
WHERE note-type = "session" AND reviewed = false
SORT date DESC
LIMIT 5
```

> *All sessions reviewed.*

### Open Research

```dataview
TABLE title, date-started, status
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment" AND (status = "Open" OR status = "In Progress")
SORT date-started DESC
LIMIT 5
```

> *No active research.*

### Unreviewed Trades

```dataview
TABLE date, time, asset, result
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND reviewed = false
SORT date DESC, time DESC
LIMIT 5
```

> *All trades reviewed.*

---

## RECENT MISTAKES

```dataview
TABLE date, asset, result, mistake
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND mistake AND mistake != ""
SORT date DESC
LIMIT 5
```

> *No mistakes flagged.*

---

## SYSTEM

| Module | Dashboard | Database |
|---|---|---|
| Trading | [[Dashboard - Trading]] | [[_Bases/Trades.base\|Trades]] |
| Strategy | [[Dashboard - Strategy]] | [[_Bases/Strategies.base\|Strategies]] |
| Research | [[Dashboard - Research]] | [[_Bases/Research.base\|Research]] |
| Market | [[Dashboard - Market]] | [[_Bases/Assets.base\|Assets]] |
| Psychology | [[Dashboard - Psychology]] | [[_Bases/Mistakes.base\|Mistakes]] |
| Reviews | [[Dashboard - Review]] | [[_Bases/Reviews.base\|Reviews]] |
| Knowledge | [[Dashboard - Knowledge]] | — |

---
*[[SYSTEM GUIDE]] · [[WORKFLOW GUIDE]] · [[DATA DICTIONARY]] · [[WALKTHROUGH]]*