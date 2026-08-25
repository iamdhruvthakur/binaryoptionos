<%*
const date = tp.date.now("YYYY-MM-DD");
const dateCompact = tp.date.now("YYYYMMDD");
const unique = Math.random().toString(36).substring(2, 6).toUpperCase();
const seq = tp.date.now("HHmmss") + "-" + unique;
const fileName = "PSY-" + dateCompact + "-" + seq;
const biasTypes = ["FOMO", "Revenge", "Overconfidence", "Fear", "Tilt", "Hesitation", "None"];
const biasType = await tp.system.suggester(biasTypes, biasTypes, false, "Bias Type:") ?? "None";
const impacts = ["Negative", "Positive", "Neutral"];
const impact = await tp.system.suggester(impacts, impacts, false, "Impact:") ?? "Neutral";
await tp.file.rename(fileName);
await tp.file.move("06-Psychology/Observations/" + fileName);
-%>
---
note-type: psychology-observation
id: <% fileName %>
date: <% date %>
session-ref: ""
trade-ref: ""
emotional-state: ""
bias-type: "<% biasType %>"
impact: "<% impact %>"
resolution: ""
tags:
  - psychology
---

# Psychology Note: <% fileName %>

> **Date:** <% date %> | **Bias:** <% biasType %> | **Impact:** <% impact %>

## Emotional State

*Describe your emotional state at the time.*

## What Happened

*What did you do, or almost do, because of this psychological state?*

## Impact on Trading

## Root Cause

*Why were you in this state?*

## Resolution / What to Do Instead

## Related Trade or Session

---
*[[Dashboard - Psychology|Psychology Dashboard]]* | *[[Dashboard - Trading OS|Home]]*