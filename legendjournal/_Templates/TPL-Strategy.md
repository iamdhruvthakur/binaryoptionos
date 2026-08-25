<%*
const date = tp.date.now("YYYY-MM-DD");
const rawName = await tp.system.prompt("Strategy Short Name (e.g. V6):") ?? "New";
const name = rawName.replace(/[^A-Za-z0-9\-\.]/g, '-').replace(/-+/g, '-');
const fileName = "STR-" + name;
await tp.file.rename(fileName);
await tp.file.move("02-Strategies/Registry/" + fileName);
-%>
---
note-type: strategy
id: <% fileName %>
name: "Strategy <% rawName %>"
status: Development
created: <% date %>
current-version: ""
versions: []
description: ""
core-concept: ""
primary-assets: []
primary-sessions: []
primary-regimes: []
tags:
  - strategy
---

# Strategy: <% rawName %>

> **Status:** Development | **Created:** <% date %>

## Core Concept

*What is the fundamental idea behind this strategy?*

## Entry Conditions

*What conditions must be met to enter a trade?*

## Exit / Expiry Rules

## Market Conditions

**Best Regimes:**
**Best Sessions:**
**Best Assets:**

## Variables Used

## Known Weaknesses

## Version History

| Version | Status | Created | Notes |
|---|---|---|---|
| | | | |

## Research

## Evidence

---
*[[Dashboard - Strategy|Strategy Dashboard]]* | *[[Dashboard - Trading OS|Home]]*