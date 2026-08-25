---
note-type: dashboard
title: Review Dashboard
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
  [[Dashboard - Psychology|PSYCHOLOGY]]
  <strong>REVIEW</strong>
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# REVIEW

<div class="tos-subtitle">Session Completion · Weekly Alignment</div>

<div class="quick-actions">

```meta-bind-button
style: primary
label: "+ DAILY REVIEW"
id: btn-daily-rev
actions:
  - type: command
    command: quickadd:choice:03-daily-review
```

```meta-bind-button
style: default
label: "+ WEEKLY REVIEW"
id: btn-weekly-rev
actions:
  - type: command
    command: quickadd:choice:04-weekly-review
```

</div>

---

## REVIEW STATUS

### Unreviewed Sessions

```dataview
TABLE date, total-trades, win-rate
FROM "01-Journal/Sessions"
WHERE note-type = "session" AND reviewed = false
SORT date DESC
```

> *All sessions reviewed!*

### Unreviewed Trades

```dataview
TABLE date, time, asset, result
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND reviewed = false
SORT date DESC, time DESC
```

> *All trades reviewed!*

---

## RECENT DAILY REVIEWS

```dataview
TABLE date, day-of-week, total-trades, win-rate, psychology-rating
FROM "01-Journal/Reviews"
WHERE note-type = "review" AND review-type = "Daily"
SORT date DESC
LIMIT 7
```

> *No daily reviews logged.*

---

## RECENT WEEKLY REVIEWS

```dataview
TABLE year, week-number, total-trades, win-rate, strategy-version
FROM "01-Journal/Reviews"
WHERE note-type = "review" AND review-type = "Weekly"
SORT year DESC, week-number DESC
LIMIT 4
```

> *No weekly reviews logged.*

---

## MISTAKE FEEDBACK (Last 14 Days)

```dataview
TABLE WITHOUT ID
  mistake as "Mistake",
  length(rows) as "Occurrences"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX" AND mistake != "" AND date >= date(today) - dur(14 days)
GROUP BY mistake
SORT length(rows) DESC
```

> *No mistakes logged in the last 14 days.*

---
*[[Dashboard - Trading OS|Home]] · [[_Bases/Reviews.base|Reviews Database]]*
