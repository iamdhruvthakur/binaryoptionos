---
note-type: dashboard
title: Knowledge Dashboard
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
  [[Dashboard - Review|REVIEW]]
  <strong>KNOWLEDGE</strong>
</div>

# KNOWLEDGE

<div class="tos-subtitle">Concepts · Rules · Facts</div>

<div class="quick-actions">

```meta-bind-button
style: default
label: "+ NEW KNOWLEDGE"
id: btn-new-knowledge
actions:
  - type: command
    command: quickadd:choice:16-new-knowledge
```

</div>

---

## CONFIRMED RULES

```dataview
TABLE title, source, status
FROM "07-Knowledge/Rules"
WHERE note-type = "knowledge" AND information-type = "RULE"
SORT title ASC
```

> *No confirmed rules recorded.*

---

## ATOMIC CONCEPTS

```dataview
TABLE title, topic, status
FROM "07-Knowledge/Concepts"
WHERE note-type = "knowledge" AND information-type = "CONCEPT"
SORT title ASC
LIMIT 10
```

> *No concepts recorded.*

---

## HYPOTHESES & UNVERIFIED IDEAS

```dataview
TABLE title, topic
FROM "07-Knowledge"
WHERE note-type = "knowledge" AND (information-type = "HYPOTHESIS" OR information-type = "UNVERIFIED-IDEA")
SORT title ASC
```

> *No unverified ideas currently logged.*

---

## PERSONAL OPINIONS

```dataview
TABLE title, topic
FROM "07-Knowledge"
WHERE note-type = "knowledge" AND information-type = "PERSONAL-OPINION"
SORT title ASC
```

> *No personal opinions recorded.*

---

## RECENTLY ADDED

```dataview
TABLE title, information-type, topic
FROM "07-Knowledge"
WHERE note-type = "knowledge"
SORT file.ctime DESC
LIMIT 5
```

> *Knowledge base is empty.*

---
*[[Dashboard - Trading OS|Home]]*
