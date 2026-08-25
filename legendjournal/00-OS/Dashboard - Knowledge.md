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

<div class="tos-subtitle">Rules · Concepts · Research Library</div>

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

> *No rules established. Rules are created when research confirms a hypothesis.*

---

## CONCEPTS

```dataview
TABLE title, information-type, source, status
FROM "07-Knowledge/Concepts"
WHERE note-type = "knowledge"
SORT information-type ASC, title ASC
```

> *No concepts recorded.*

---

## BY INFORMATION TYPE

```dataview
TABLE WITHOUT ID
  information-type as "Type",
  length(rows) as "Count"
FROM "07-Knowledge"
WHERE note-type = "knowledge"
GROUP BY information-type
SORT length(rows) DESC
```

> *No knowledge notes. The knowledge system tracks the progression from observation to confirmed rule.*

---

## IMPORTED KNOWLEDGE

```dataview
TABLE title, information-type, migrated-from, status
FROM "07-Knowledge/Imported"
WHERE note-type = "knowledge"
SORT title ASC
```

> *No imported knowledge yet.*

---

## RECENT KNOWLEDGE

```dataview
TABLE title, information-type, source, status
FROM "07-Knowledge"
WHERE note-type = "knowledge"
SORT file.ctime DESC
LIMIT 10
```

> *No knowledge notes created.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Research|Research]] · [[SYSTEM GUIDE]]*
