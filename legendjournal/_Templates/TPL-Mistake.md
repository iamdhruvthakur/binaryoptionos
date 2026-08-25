<%*
const date = tp.date.now("YYYY-MM-DD");
const rawName = await tp.system.prompt("Mistake short name (e.g. Early-Entry):") ?? "New-Mistake";
const name = rawName.replace(/ /g, '-').replace(/[^A-Za-z0-9\-]/g, '');
const categories = ["Execution", "Psychology", "Analysis", "Risk", "Timing"];
const category = await tp.system.suggester(categories, categories, false, "Category:") ?? "Execution";
const fileName = "MST-" + name;
await tp.file.rename(fileName);
await tp.file.move("06-Psychology/Mistakes/" + fileName);
-%>
---
note-type: mistake
id: <% fileName %>
name: "<% rawName %>"
category: "<% category %>"
description: ""
frequency: 0
resolution: ""
status: Open
associated-strategies: []
associated-regimes: []
associated-sessions: []
associated-variables: []
tags:
  - mistake
---

# Mistake: <% rawName %>

> **Category:** <% category %> | **Status:** Open

## Description

*Describe this mistake precisely. What behaviour does it represent?*

## How to Identify

*How do you know when you've made this mistake?*

## Root Cause

*Why does this mistake happen?*

## Resolution / Correction

*What is the correct behaviour? What rule prevents this mistake?*

## Occurrences

*Link to trades where this mistake occurred.*

## Pattern Notes

*When does this mistake most commonly happen? Which sessions, regimes, mental states?*

---
*[[Dashboard - Psychology|Psychology Dashboard]]* | *[[Dashboard - Trading OS|Home]]*