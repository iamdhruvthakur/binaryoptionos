<%*
const rawName = await tp.system.prompt("Asset name (e.g. EUR-USD):") ?? "UNSET";
const name = rawName.replace(/\//g, '-').replace(/[^A-Za-z0-9\-]/g, '');
const assetClasses = ["Forex", "Crypto", "Commodity", "Index", "Stock"];
const assetClass = await tp.system.suggester(assetClasses, assetClasses, false, "Asset Class:") ?? "Forex";
const marketTypes = ["Live", "OTC"];
const marketType = await tp.system.suggester(marketTypes, marketTypes, false, "Market Type:") ?? "Live";
const fileName = "AST-" + name;
await tp.file.rename(fileName);
await tp.file.move("04-Market/Assets/" + fileName);
-%>
---
note-type: asset
id: <% fileName %>
name: "<% rawName %>"
alias: "<% name %>"
asset-class: "<% assetClass %>"
asset-type: "<% marketType %>"
typical-sessions: []
behaviour-notes: ""
tags:
  - asset
  - reference
---

# Asset: <% name %>

**Class:** <% assetClass %>

## Characteristics

*Describe this asset's typical behaviour, volatility, spread characteristics.*

## Best Sessions for This Asset

## Regime Behaviour

| Regime | Behaviour | Strategy Suitability |
|---|---|---|
| Normal | | |
| Reversal | | |
| Choppy | | |
| Trending | | |

## Notes

---
*[[Dashboard - Market|Market Dashboard]]* | *[[Dashboard - Trading OS|Home]]*