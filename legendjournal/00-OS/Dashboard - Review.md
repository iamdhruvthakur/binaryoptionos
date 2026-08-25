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

<div class="tos-subtitle">Daily Reviews · Weekly Reviews · Discipline Tracking</div>

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
TABLE date, session-type, total-trades, win-rate
FROM "01-Journal/Sessions"
WHERE note-type = "session" AND reviewed = false
SORT date DESC
```

> *All sessions reviewed.*

### Unreviewed Trades

```dataview
TABLE date, time, asset, direction, result
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND reviewed = false
SORT date DESC, time DESC
LIMIT 10
```

> *All trades reviewed.*

---

## DAILY REVIEWS

```dataview
TABLE date, day-of-week, total-trades, wins, losses, win-rate, psychology-rating
FROM "01-Journal/Reviews"
WHERE note-type = "review" AND review-type = "Daily"
SORT date DESC
LIMIT 14
```

> *No daily reviews. Use **+ DAILY REVIEW** to create one.*

---

## WEEKLY REVIEWS

```dataview
TABLE week-number, year, total-trades, win-rate, strategy-version, key-discoveries
FROM "01-Journal/Reviews"
WHERE note-type = "review" AND review-type = "Weekly"
SORT year DESC, week-number DESC
LIMIT 10
```

> *No weekly reviews yet.*

---

## CONSISTENCY (LAST 30 DAYS)

```dataview
TABLE date, total-trades, wins, losses, win-rate, psychology-rating
FROM "01-Journal/Reviews"
WHERE note-type = "review" AND review-type = "Daily" AND date >= date(today) - dur(30 days)
SORT date DESC
```

> *No reviews in the last 30 days. Consistent reviewing is critical for improvement.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Psychology|Psychology]] · [[_Bases/Reviews.base|Reviews Database]]*
