<%*
const date = tp.date.now("YYYY-MM-DD");
const rawTitle = await tp.system.prompt("Knowledge note title:") ?? "Untitled";
const infoTypes = ["FACT", "RULE", "HYPOTHESIS", "OBSERVATION", "EXPERIMENT", "CONCLUSION", "PERSONAL-OPINION", "UNVERIFIED-IDEA"];
const infoType = await tp.system.suggester(infoTypes, infoTypes, false, "Information Type:") ?? "OBSERVATION";
const fileName = "KNW-" + rawTitle.replace(/ /g, '-').replace(/[^A-Za-z0-9\-]/g, '');
await tp.file.rename(fileName);
if (infoType === "RULE") {
  await tp.file.move("07-Knowledge/Rules/" + fileName);
} else {
  await tp.file.move("07-Knowledge/Concepts/" + fileName);
}
-%>
---
note-type: knowledge
id: <% fileName %>
title: "<% rawTitle %>"
information-type: "<% infoType %>"
source: ""
topic: ""
strategy-relevance: []
variable-relevance: []
status: Current
migrated-from: ""
tags:
  - knowledge
---

> [!important] Information Type: <% infoType %>
> This note is classified as **<% infoType %>**. This classification should be accurate — do not mark as RULE unless it is a confirmed, tested rule.

# <% rawTitle %>

## Content

*Write the knowledge content here.*

## Source

*Where does this knowledge come from? Observation, research, external source?*

## Relevance

**Related Strategy:**
**Related Variables:**
**Related Research:**

## Status Notes

---
*[[Dashboard - Trading OS|Home]]*