<%*
const date = tp.date.now("YYYY-MM-DD");
const dateCompact = tp.date.now("YYYYMMDD");
const unique = Math.random().toString(36).substring(2, 6).toUpperCase();
const seq = tp.date.now("HHmmss") + "-" + unique;
const fileName = "EVD-" + dateCompact + "-" + seq;
const evidenceTypes = ["Screenshot", "Chart", "Annotation", "Document", "Video"];
const evidenceType = await tp.system.suggester(evidenceTypes, evidenceTypes, false, "Evidence Type:") ?? "Screenshot";
await tp.file.rename(fileName);
await tp.file.move("08-Evidence/" + fileName);
-%>
---
note-type: evidence
id: <% fileName %>
date: <% date %>
evidence-type: "<% evidenceType %>"
asset: ""
session: ""
trade-ref: ""
strategy-version: ""
market-regime: ""
description: ""
tags:
  - evidence
---

# Evidence: <% fileName %>

> **Type:** <% evidenceType %> | **Date:** <% date %>

## Description

*Describe what this evidence shows.*

## Image / Attachment

*Paste image here or drag from 08-Evidence/Attachments/*

## Context

**Asset:**
**Session:**
**Market Regime:**
**Strategy Version:**

## What This Evidence Shows

## Links

**Linked Trade:**
**Linked Research:**
**Linked Observation:**

---
*[[Dashboard - Trading OS|Home]]*