<%*
const date = tp.date.now("YYYY-MM-DD");
const rawName = await tp.system.prompt("Variable name:") ?? "UNSET";
const rawAlias = await tp.system.prompt("Short alias:") ?? rawName;
const alias = rawAlias.replace(/ /g, '-').replace(/[^A-Za-z0-9\-]/g, '');
const categories = ["Primary", "Secondary", "Confluence", "Event", "Filter"];
const category = await tp.system.suggester(categories, categories, false, "Category:") ?? "Primary";
const fileName = "VAR-" + alias;
await tp.file.rename(fileName);
await tp.file.move("05-Variables/" + fileName);
-%>
---
note-type: variable
id: <% fileName %>
name: "<% rawName %>"
alias: "<% alias %>"
category: "<% category %>"
description: ""
rules: ""
strategy-versions: []
evidence: []
tags:
  - variable
  - reference
---

# Variable: <% rawName %>

**Category:** <% category %> | **Alias:** <% alias %>

## Definition

*Provide a precise, unambiguous definition of this variable.*

## How to Identify

*Exact identification criteria.*

## Rules

*Trading rules associated with this variable. Mark clearly as RULE.*

## Performance Notes

*How does this variable perform? Under what conditions?*

## Evidence

## Related Research

---
*[[Dashboard - Trading OS|Home]]*