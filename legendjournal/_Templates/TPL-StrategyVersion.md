<%*
const date = tp.date.now("YYYY-MM-DD");
const rawVersion = await tp.system.prompt("Version number (e.g. 6.2):") ?? "";
const version = rawVersion.replace(/^[Vv]/, '');
const fileName = "VER-V" + version;
await tp.file.rename(fileName);
await tp.file.move("02-Strategies/Versions/" + fileName);
-%>
---
note-type: strategy-version
id: <% fileName %>
strategy: "[[STR-V6]]"
version: "<% version %>"
status: Testing
created: <% date %>
superseded-by: ""
supersedes: ""
variables: []
changelog: ""
backtest-count: 0
live-trade-count: 0
win-rate: 0
tags:
  - strategy-version
---

# Strategy Version <% version %>

> **Status:** Testing | **Created:** <% date %>

## Summary of Changes

*What changed in this version from the previous?*

## Full Rule Set

### Entry Rules

### Variable Requirements

### Market Conditions

### Risk Rules

## Performance Summary

| Metric | Backtest | Live |
|---|---|---|
| Total Trades | | |
| Win Rate | | |
| Best Regime | | |
| Best Asset | | |

## Backtest Results

*Link to Backtest notes here.*

## Live Trade Results

*Populated automatically via Dataview.*

## Known Issues

## Evidence

---
*[[Dashboard - Strategy|Strategy Dashboard]]* | *[[Dashboard - Trading OS|Home]]*