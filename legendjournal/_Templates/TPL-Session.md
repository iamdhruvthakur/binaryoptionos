<%*
const date = tp.date.now("YYYY-MM-DD");
const dateCompact = tp.date.now("YYYYMMDD");
const year = tp.date.now("YYYY");
const dayName = tp.date.now("dddd");
const unique = Math.random().toString(36).substring(2, 6).toUpperCase();
const seq = tp.date.now("HHmm") + "-" + unique;
const fileName = "SES-" + dateCompact + "-" + seq;

const sessionTypes = ["London", "New York", "Asian", "London-NY Overlap", "Pre-Market", "Post-Market", "OTC"];
const sessionType = await tp.system.suggester(sessionTypes, sessionTypes, false, "Session Type:") ?? "UNSET";

const regimes = ["Normal", "Reversal", "Choppy", "Trending"];
const regime = await tp.system.suggester(regimes, regimes, false, "Market Regime:") ?? "UNSET";

const sessionSlug = sessionType.replace(/ /g, '-');
const regimeSlug = regime;

await tp.file.rename(fileName);
await tp.file.move("01-Journal/Sessions/" + year + "/" + fileName);
-%>
---
note-type: session
id: <% fileName %>
date: <% date %>
day-of-week: <% dayName %>
session-type: "[[SES-TYPE-<% sessionSlug %>]]"
market-regime: "[[REG-<% regimeSlug %>]]"
start-time: ""
end-time: ""
assets-traded: []
strategy-version: ""
total-trades: 0
wins: 0
losses: 0
voids: 0
win-rate: 0
net-result: ""
net-pl: 0
mental-state: ""
session-notes: ""
reviewed: false
review-ref: ""
trades: []
evidence: []
tags:
  - session
---

> [!info] Session: <% fileName %>
> **Date:** <% date %> (<% dayName %>) | **Session:** <% sessionType %> | **Regime:** <% regime %>

## Pre-Session

**Mental State:**

**Market Bias:**

**Key Levels to Watch:**

## Session Log

*Record trades as they happen. Link to trade notes.*

| Time | Asset | Direction | Result | Trade Note |
|---|---|---|---|---|
| | | | | |

## Session Summary

**Total Trades:**
**Wins:**
**Losses:**
**Win Rate:**

## Key Observations

## Mistakes This Session

## Market Notes

## Evidence

---
*[[Dashboard - Trading OS|Home]]* | *[[Dashboard - Trading|Trades Database]]*