---
note-type: dashboard
title: Strategy Dashboard
cssclasses:
  - dashboard
tags:
  - dashboard
---

<div class="tos-nav">
  [[Dashboard - Trading OS|HOME]]
  [[Dashboard - Trading|TRADING]]
  <strong>STRATEGY</strong>
  [[Dashboard - Research|RESEARCH]]
  [[Dashboard - Market|MARKET]]
  [[Dashboard - Psychology|PSYCHOLOGY]]
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# STRATEGY

<div class="tos-subtitle">Registry · Version Control · Confluences</div>

<div class="quick-actions">

```meta-bind-button
style: default
label: "+ NEW VERSION"
id: btn-new-version
actions:
  - type: command
    command: quickadd:choice:06-new-strategy-version
```

```meta-bind-button
style: default
label: "+ CHANGELOG"
id: btn-new-changelog
actions:
  - type: command
    command: quickadd:choice:07-new-changelog
```

```meta-bind-button
style: default
label: "+ BACKTEST"
id: btn-new-backtest
actions:
  - type: command
    command: quickadd:choice:09-new-backtest
```

</div>

---

## ACTIVE STRATEGIES

```dataview
TABLE status, current-version, core-concept
FROM "02-Strategies/Registry"
WHERE note-type = "strategy" AND status = "Active"
SORT name ASC
```

> *No active strategies registered.*

---

## STRATEGY VERSIONS

```dataview
TABLE version, status, created, backtest-count, live-trade-count, win-rate
FROM "02-Strategies/Versions"
WHERE note-type = "strategy-version"
SORT version DESC
```

> *No strategy versions found.*

---

## PERFORMANCE BY VERSION

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

> *No live trades recorded against any version.*

---

## RECENT CHANGES

```dataview
TABLE date, from-version, to-version, change-type, change-summary
FROM "02-Strategies/Changelogs"
WHERE note-type = "strategy-changelog"
SORT date DESC
LIMIT 10
```

> *No changelogs recorded. Document strategy evolution using **+ CHANGELOG**.*

---

## VARIABLES & CONFLUENCES

```dataview
TABLE name, category, alias
FROM "05-Variables"
WHERE note-type = "variable"
SORT category ASC
```

> *No variables registered.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Trading|Trading]] · [[_Bases/Strategies.base|Strategy Database]]*
