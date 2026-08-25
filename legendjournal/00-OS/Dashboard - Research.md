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

<div class="tos-subtitle">Experiments · Backtests · Observations · Evidence</div>

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

## PIPELINE

```dataview
TABLE WITHOUT ID
  status as "Status",
  length(rows) as "Count"
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment"
GROUP BY status
```

> *No experiments in the pipeline. Start with **+ NEW EXPERIMENT**.*

---

## CANDLE BEHAVIOR RESEARCH

```dataview
TABLE WITHOUT ID
  candle-behavior as "Candle Behavior",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND candle-behavior != null AND candle-behavior != ""
GROUP BY candle-behavior
SORT length(rows) DESC
LIMIT 10
```

> *No candle behavior data available.*

---

## SEQUENCE RESEARCH

```dataview
TABLE WITHOUT ID
  sequence as "Sequence",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND sequence != null AND sequence != ""
GROUP BY sequence
SORT length(rows) DESC
LIMIT 10
```

> *No sequence data available.*

---

## PATTERN RESEARCH

```dataview
TABLE WITHOUT ID
  pattern as "Pattern",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND pattern != null AND pattern != ""
GROUP BY pattern
SORT length(rows) DESC
LIMIT 10
```

> *No pattern data available.*

---

## ACTIVE EXPERIMENTS

```dataview
TABLE title, date-started, strategy-version, hypothesis, sample-size
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment" AND (status = "Open" OR status = "In Progress")
SORT date-started DESC
```

> *No active experiments.*

---

## COMPLETED RESEARCH

```dataview
TABLE title, date-completed, conclusion-type, conclusion
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment" AND status = "Completed"
SORT date-completed DESC
```

> *No completed research yet.*

---

## CONFIRMED FINDINGS

```dataview
TABLE title, conclusion
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment" AND conclusion-type = "CONFIRMED"
```

> *No confirmed findings. Confirmed experiments become trading rules.*

---

## REJECTED HYPOTHESES

```dataview
TABLE title, conclusion
FROM "03-Research/Experiments"
WHERE note-type = "research-experiment" AND conclusion-type = "REFUTED"
```

> *No rejected hypotheses.*

---

## BACKTESTS

```dataview
TABLE date-run, strategy-version, asset, market-regime, total-trades, win-rate
FROM "03-Research/Backtests"
WHERE note-type = "backtest"
SORT date-run DESC
```

> *No backtests completed yet.*

---

## RECENT OBSERVATIONS

```dataview
TABLE date, observation-type, information-type, summary, status
FROM "03-Research/Observations"
WHERE note-type = "observation"
SORT date DESC
LIMIT 10
```

> *No observations recorded. Use **+ OBSERVATION** to log market or system observations.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Strategy|Strategy]] · [[_Bases/Research.base|Research Database]]*
