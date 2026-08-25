<%*
const date = tp.date.now("YYYY-MM-DD");
const dateCompact = tp.date.now("YYYYMMDD");
const unique = Math.random().toString(36).substring(2, 6).toUpperCase();
const seq = tp.date.now("HHmmss") + "-" + unique;
const fileName = "OBS-" + dateCompact + "-" + seq;
const obsTypes = ["Market", "Candle", "Session", "Asset", "Variable", "System"];
const obsType = await tp.system.suggester(obsTypes, obsTypes, false, "Observation Type:") ?? "Market";
const infoTypes = ["OBSERVATION", "FACT", "HYPOTHESIS", "UNVERIFIED-IDEA"];
const infoType = await tp.system.suggester(infoTypes, infoTypes, false, "Information Type:") ?? "OBSERVATION";
await tp.file.rename(fileName);
await tp.file.move("03-Research/Observations/" + fileName);
-%>
---
note-type: observation
id: <% fileName %>
date: <% date %>
observation-type: "<% obsType %>"
information-type: "<% infoType %>"
asset: []
session: []
market-regime: []
strategy: []
variables: []
summary: ""
evidence: []
status: Open
tags:
  - observation
---

> [!note] <% infoType %>: <% obsType %> Observation -- <% date %>

# Observation: <% fileName %>

## Observation

*Describe exactly what you observed. Be specific and factual.*

**Information Type:** <% infoType %>

> Note: This is marked as <% infoType %>. Do not elevate this to RULE or CONCLUSION without evidence.

## Context

**Date:** <% date %>
**Asset(s):**
**Session:**
**Market Regime:**

## Evidence

## Potential Implications

*What might this observation suggest? (Keep this speculative -- do not claim certainty.)*

## Related Research

## Status Updates

---
*[[Dashboard - Research|Research Dashboard]]* | *[[Dashboard - Trading OS|Home]]*