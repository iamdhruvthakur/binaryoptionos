---
note-type: dashboard
title: Psychology Dashboard
cssclasses:
  - dashboard
tags:
  - dashboard
---

<div class="tos-nav">
  [[Dashboard - Trading OS|HOME]]
  [[Dashboard - Trading|TRADING]]
  [[Dashboard - Strategy|STRATEGY]]
  [[Dashboard - Research|RESEARCH]]
  [[Dashboard - Market|MARKET]]
  <strong>PSYCHOLOGY</strong>
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# PSYCHOLOGY

<div class="tos-subtitle">Mental Capital · Mistakes · Observations</div>

<div class="quick-actions">

```meta-bind-button
style: default
label: "+ NEW MISTAKE"
id: btn-new-mistake
actions:
  - type: command
    command: quickadd:choice:11-new-mistake
```

```meta-bind-button
style: default
label: "+ PSYCHOLOGY NOTE"
id: btn-new-psych
actions:
  - type: command
    command: quickadd:choice:12-new-psychology
```

</div>

---

## MISTAKE REGISTRY

```dataview
TABLE name, category, frequency, status, resolution
FROM "06-Psychology/Mistakes"
WHERE note-type = "mistake"
SORT frequency DESC
```

> *No mistakes registered.*

---

## ALL-TIME MISTAKE IMPACT

```dataview
TABLE WITHOUT ID
  mistake as "Mistake",
  length(rows) as "Occurrences",
  length(filter(rows, (r) => r.result = "LOSS")) as "Losses",
  round(length(filter(rows, (r) => r.result = "LOSS")) / max(length(rows), 1) * 100, 0) + "%" as "Loss Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND mistake != ""
GROUP BY mistake
SORT length(rows) DESC
```

> *No mistake impact data available.*

---

## RECENT TRADES WITH PSYCH FLAGS

```dataview
TABLE date, time, asset, result, mistake, psychology-note
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND psychology-flag = true
SORT date DESC
LIMIT 10
```

> *No recent trades flagged for psychology.*

---

## RECENT PSYCHOLOGY OBSERVATIONS

```dataview
TABLE date, emotional-state, bias-type, impact
FROM "06-Psychology/Observations"
WHERE note-type = "psychology-observation"
SORT date DESC
LIMIT 5
```

> *No recent psychology observations.*

---

## RECENT MISTAKE OCCURRENCES

```dataview
TABLE date, time, asset, result, mistake
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND mistake != ""
SORT date DESC
LIMIT 10
```

> *No recent mistakes recorded.*

---
*[[Dashboard - Trading OS|Home]] · [[_Bases/Mistakes.base|Mistakes Database]]*
