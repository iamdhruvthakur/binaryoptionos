<%*
const date = tp.date.now("YYYY-MM-DD");
const rawVersion = await tp.system.prompt("New version (e.g. V6.2):") ?? "";
const version = rawVersion.replace(/^[Vv]/, '').replace(/[^A-Za-z0-9\.\-]/g, '');
const fileName = "CL-V" + version;
const changeTypes = ["Addition", "Removal", "Modification", "Restructure"];
const changeType = await tp.system.suggester(changeTypes, changeTypes, false, "Change Type:") ?? "Modification";
await tp.file.rename(fileName);
await tp.file.move("02-Strategies/Changelogs/" + fileName);
-%>
---
note-type: strategy-changelog
id: <% fileName %>
date: <% date %>
strategy: "[[STR-V6]]"
from-version: ""
to-version: "[[VER-V<% version %>]]"
change-type: "<% changeType %>"
reason: ""
change-summary: ""
evidence: []
tags:
  - changelog
---

# Changelog: V<% version %>

> **Date:** <% date %> | **Type:** <% changeType %>

## What Changed

*Describe what was added, removed, or modified.*

## Why It Changed

*What triggered this change? Evidence, research, or observation?*

## Before

*Document the previous state / rules.*

## After

*Document the new state / rules.*

## Supporting Evidence

## Impact Assessment

---
*[[Dashboard - Strategy|Strategy Dashboard]]* | *[[Dashboard - Trading OS|Home]]*