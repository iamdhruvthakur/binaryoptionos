<%*
const date = tp.date.now("YYYY-MM-DD");
const dateCompact = tp.date.now("YYYYMMDD");
const unique = Math.random().toString(36).substring(2, 6).toUpperCase();
const seq = tp.date.now("HHmmss") + "-" + unique;
const fileName = "EXP-" + dateCompact + "-" + seq;
await tp.file.rename(fileName);
await tp.file.move("03-Research/Experiments/" + fileName);
-%>
---
note-type: research-experiment
id: <% fileName %>
title: ""
date-started: <% date %>
date-completed: ""
status: Open
hypothesis: ""
method: ""
dataset-description: ""
strategy: "[[STR-V6]]"
strategy-version: ""
variables: []
market-regimes: []
assets: []
sessions: []
sample-size: 0
result: ""
conclusion: ""
conclusion-type: ""
evidence: []
related-experiments: []
tags:
  - research
---

# Research Experiment: <% fileName %>

> **Status:** Open | **Started:** <% date %>

## Research Question

*What are you trying to find out?*

## Hypothesis

> [!quote] Hypothesis
> *State your hypothesis clearly and specifically.*

**Type:** HYPOTHESIS

## Reason for Research

*Why is this question important? What triggered this investigation?*

## Method

*How will you test this? What data will you use? What is the sample size?*

## Variables Being Tested

## Dataset / Evidence

*What data, trades, or observations will you use?*

## Observations

*Record observations as you conduct the research.*

## Results

**Sample Size:**
**Data Period:**

## Conclusion

> [!note] Conclusion
> *State your conclusion clearly. Is the hypothesis confirmed, refuted, or inconclusive?*

**Type:** -- (CONFIRMED / REFUTED / INCONCLUSIVE / PARTIAL)

**Confidence:**

## Next Actions

## Related Research

---
*[[Dashboard - Research|Research Dashboard]]* | *[[Dashboard - Trading OS|Home]]*