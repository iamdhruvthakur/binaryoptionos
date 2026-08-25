<%*
const date = tp.date.now("YYYY-MM-DD");
const year = tp.date.now("YYYY");
const dayName = tp.date.now("dddd");
const fileName = "REV-D-" + date;
await tp.file.rename(fileName);
await tp.file.move("01-Journal/Reviews/" + year + "/" + fileName);
-%>
---
note-type: review
id: <% fileName %>
review-type: Daily
date: <% date %>
day-of-week: <% dayName %>
session-refs: []
trade-refs: []
total-trades: 0
wins: 0
losses: 0
win-rate: 0
key-observations: ""
mistakes-identified: []
psychology-rating: 3
what-went-well: ""
what-to-improve: ""
tags:
  - review
  - daily-review
---

# Daily Review — <% dayName %>, <% date %>

## Performance Summary

| Metric | Value |
|---|---|
| Total Trades | |
| Wins | |
| Losses | |
| Win Rate | % |
| Psychology Rating | /5 |

## Sessions Today

*Link to session notes here.*

## Trades Today

*Link to trade notes here.*

## What Went Well

## What to Improve

## Key Observations

## Mistakes Identified

*Link to Mistake notes if applicable.*

## Psychology Notes

**State before trading:**

**State during trading:**

**Overall rating (1-5):**

## Notes & Reflections

---
*[[Dashboard - Review|Reviews]]* | *[[Dashboard - Trading OS|Home]]*