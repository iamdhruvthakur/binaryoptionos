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
  [[Dashboard - Binary Options|BINARY]]
  [[Dashboard - Trading|TRADING]]
  [[Dashboard - Strategy|STRATEGY]]
  [[Dashboard - Research|RESEARCH]]
  [[Dashboard - Market|MARKET]]
  <strong>PSYCHOLOGY</strong>
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# PSYCHOLOGY

<div class="tos-subtitle">Mistakes · Biases · Emotional Patterns · Self-Awareness</div>

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

> *No mistakes recorded. Identifying mistakes is the first step to improving.*

---

## MISTAKE IMPACT (FROM TRADES)

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

## PSYCHOLOGY-FLAGGED TRADES

```dataview
TABLE date, asset, direction, result, psychology-note, mistake
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND psychology-flag = true
SORT date DESC
LIMIT 15
```

> *No psychology-flagged trades. Flag trades where emotions influenced decisions.*

---

## BIAS FREQUENCY

```dataview
TABLE WITHOUT ID
  bias-type as "Bias",
  length(rows) as "Count",
  length(filter(rows, (r) => r.impact = "Negative")) as "Negative Impact"
FROM "06-Psychology/Observations"
WHERE note-type = "psychology-observation"
GROUP BY bias-type
SORT length(rows) DESC
```

> *No bias data available.*

---

## PSYCHOLOGY OBSERVATIONS

```dataview
TABLE date, bias-type, impact, emotional-state
FROM "06-Psychology/Observations"
WHERE note-type = "psychology-observation"
SORT date DESC
LIMIT 10
```

> *No psychology observations. Use **+ PSYCHOLOGY NOTE** to log emotional patterns.*

---

## PSYCHOLOGY RATING TREND

```dataview
TABLE date, day-of-week, psychology-rating, total-trades, win-rate
FROM "01-Journal/Reviews"
WHERE note-type = "review" AND review-type = "Daily"
SORT date DESC
LIMIT 14
```

> *No daily reviews. Psychology ratings are captured during daily reviews.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Review|Review]] · [[_Bases/Mistakes.base|Mistakes Database]]*
