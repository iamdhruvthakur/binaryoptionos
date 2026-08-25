<%*
const date = tp.date.now("YYYY-MM-DD");
const year = tp.date.now("YYYY");
const weekNum = tp.date.now("WW");
const fileName = "REV-W-" + year + "-W" + weekNum;
await tp.file.rename(fileName);
await tp.file.move("01-Journal/Reviews/" + year + "/" + fileName);
-%>
---
note-type: review
id: <% fileName %>
review-type: Weekly
week-number: "<% weekNum %>"
year: "<% year %>"
date-start: ""
date-end: ""
daily-reviews: []
total-trades: 0
wins: 0
losses: 0
win-rate: 0
strategy-version: ""
regime-summary: ""
key-discoveries: ""
strategy-adjustments: ""
goals-next-week: ""
tags:
  - review
  - weekly-review
---

# Weekly Review — Week <% weekNum %>, <% year %>

## Week Summary

| Metric | Value |
|---|---|
| Total Trades | |
| Wins | |
| Losses | |
| Win Rate | % |
| Best Session | |
| Worst Session | |

## Daily Reviews This Week

*Link to daily reviews here.*

## Performance by Regime

| Regime | Trades | W | L | WR% |
|---|---|---|---|---|
| Normal | | | | |
| Reversal | | | | |
| Choppy | | | | |
| Trending | | | | |

## Performance by Asset

## Performance by Variable

## Key Discoveries

## Strategy Notes

## Recurring Mistakes

## Goals for Next Week

---
*[[Dashboard - Review|Reviews]]* | *[[Dashboard - Trading OS|Home]]*