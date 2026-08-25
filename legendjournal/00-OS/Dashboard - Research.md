---
note-type: dashboard
title: Research Dashboard
cssclasses:
  - dashboard
tags:
  - dashboard
---

<div class="tos-nav">
  [[Dashboard - Trading OS|HOME]]
  [[Dashboard - Trading|TRADING]]
  [[Dashboard - Strategy|STRATEGY]]
  <strong>RESEARCH</strong>
  [[Dashboard - Market|MARKET]]
  [[Dashboard - Psychology|PSYCHOLOGY]]
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# RESEARCH

<div class="tos-subtitle">OTC Market Structure · Sequences · Experiments</div>

<div class="quick-actions">

```meta-bind-button
style: primary
label: "+ NEW EXPERIMENT"
id: btn-new-exp
actions:
  - type: command
    command: quickadd:choice:08-new-research
```

```meta-bind-button
style: default
label: "+ BACKTEST"
id: btn-backtest
actions:
  - type: command
    command: quickadd:choice:09-new-backtest
```

```meta-bind-button
style: default
label: "+ OBSERVATION"
id: btn-obs
actions:
  - type: command
    command: quickadd:choice:10-new-observation
```

```meta-bind-button
style: default
label: "+ EVIDENCE"
id: btn-evidence
actions:
  - type: command
    command: quickadd:choice:13-new-evidence
```

</div>

---

## DEEP RESEARCH LOOP

### By Candle Behavior

```dataview
TABLE WITHOUT ID
  candle-behavior as "Candle Behavior",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND candle-behavior != null AND candle-behavior != ""
GROUP BY candle-behavior
SORT length(rows) DESC
```

### By Sequence

```dataview
TABLE WITHOUT ID
  sequence as "Sequence",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND sequence != null AND sequence != ""
GROUP BY sequence
SORT length(rows) DESC
```

### By Pattern

```dataview
TABLE WITHOUT ID
  pattern as "Pattern",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND pattern != null AND pattern != ""
GROUP BY pattern
SORT length(rows) DESC
```

---

## PIPELINE

```dataview
TABLE WITHOUT ID
  status as "Status",
  length(rows) as "Count"
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment"
GROUP BY status
```

---

## ACTIVE EXPERIMENTS

```dataview
TABLE date-started, hypothesis
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment" AND (status = "Open" OR status = "In Progress")
SORT date-started DESC
```

> *No active experiments. Test a new hypothesis using **+ NEW EXPERIMENT**.*

---

## RECENT OBSERVATIONS

```dataview
TABLE date, observation-type, information-type, summary
FROM "03-Research/Observations"
WHERE note-type = "observation"
SORT date DESC
LIMIT 10
```

> *No recent market observations.*

---

## RECENT CONCLUSIONS

```dataview
TABLE date-completed, hypothesis, conclusion, conclusion-type
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment" AND status = "Completed"
SORT date-completed DESC
LIMIT 5
```

> *No completed experiments.*

---

## BACKTESTS

```dataview
TABLE date-run, strategy-version, asset, market-regime, total-trades, win-rate, conclusion
FROM "03-Research/Backtests"
WHERE note-type = "backtest"
SORT date-run DESC
LIMIT 10
```

> *No backtests completed. Use **+ BACKTEST** to record one.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Trading|Trading]] · [[_Bases/Research.base|Research Database]]*
