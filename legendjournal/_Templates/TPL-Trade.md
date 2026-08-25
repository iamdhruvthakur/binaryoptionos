<%*
const date = tp.date.now("YYYY-MM-DD");
const time = tp.date.now("HH:mm");
const dateCompact = tp.date.now("YYYYMMDD");
const year = tp.date.now("YYYY");
const dayName = tp.date.now("dddd");
const unique = Math.random().toString(36).substring(2, 6).toUpperCase();
const seq = tp.date.now("HHmmss") + "-" + unique;
const fileName = "TRD-" + dateCompact + "-" + seq;

const tradeType = "BINARY";

const assets = ["EUR-USD", "GBP-USD", "USD-JPY", "AUD-USD", "EUR-GBP", "USD-CAD", "BTC-USD", "GOLD", "OIL", "EUR-USD-OTC", "GBP-USD-OTC", "AUD-USD-OTC"];
const asset = await tp.system.suggester(assets, assets, false, "Select Asset:") ?? "UNSET";

let assetType = "Live";
const assetFile = app.metadataCache.getFirstLinkpathDest("AST-" + asset, "");
if (assetFile) {
    const cache = app.metadataCache.getFileCache(assetFile);
    if (cache && cache.frontmatter && cache.frontmatter["asset-type"]) {
        assetType = cache.frontmatter["asset-type"];
    }
}

let behavior = "NA";
if (assetType === "OTC") {
    const behaviors = ["NORMAL", "REVERSAL", "UNKNOWN"];
    behavior = await tp.system.suggester(behaviors, behaviors, false, "Market Behavior (OTC):") ?? "UNKNOWN";
}

const directions = ["CALL", "PUT"];
const direction = await tp.system.suggester(directions, directions, false, "Direction:") ?? "UNSET";

const results = ["WIN", "LOSS", "VOID", "BREAK-EVEN"];
const result = await tp.system.suggester(results, results, false, "Result (or skip):") ?? "";

await tp.file.rename(fileName);
await tp.file.move("01-Journal/Trades/" + year + "/" + fileName);
-%>
---
note-type: trade
id: <% fileName %>
trade-type: "<% tradeType %>"
date: <% date %>
time: "<% time %>"
day-of-week: <% dayName %>
asset: "[[AST-<% asset %>]]"
session: ""
strategy: "[[STR-V6]]"
strategy-version: ""
setup: ""
direction: "<% direction %>"
expiry: "5m"
market-regime: ""
market-behavior: "<% behavior !== 'NA' ? '[[BEH-' + behavior + ']]' : '' %>"
candle-behavior: ""
sequence: ""
pattern: ""
variables: []
result: "<% result %>"
payout: 85
stake: 10
net-pl: 0
mistake: ""
psychology-flag: false
psychology-note: ""
evidence: []
session-ref: ""
reviewed: false
review-ref: ""
tags:
  - trade
---

> [!info] Trade: <% fileName %>
> **Date:** <% date %> (<% dayName %>) | **Time:** <% time %> | **Asset:** <% asset %> | **Direction:** <% direction %>

## Trade Context

*What was the market doing? What was the context that led to this trade?*

## Setup Description

*Describe the setup. Which variables confirmed? What did the chart show?*

**Variables Present:**
- [ ] SNR (Support & Resistance) -- [[VAR-SNR]]
- [ ] Short Variable -- [[VAR-Short]]
- [ ] Sub Variable -- [[VAR-Sub]]
- [ ] Events -- [[VAR-Events]]
- [ ] Acceleration -- [[VAR-Acceleration]]
- [ ] Line / Confluence -- [[VAR-Line-Confluence]]

## Entry Analysis

*Why did you enter at this specific price/time?*

## Trade Outcome

**Result:** <% result %>
**Payout:** 85%
**Stake:** 10

## Post-Trade Analysis

*Was your analysis correct? What did price actually do? What should you have seen differently?*

## Evidence

*Add screenshots here or link to Evidence notes.*

## Notes & Lessons

---
*[[Dashboard - Trading OS|Home]]* | *[[Dashboard - Trading|Trades Database]]*