---
note-type: asset
id: AST-EUR-USD-OTC
name: EUR/USD OTC
alias: EUR-USD-OTC
asset-class: Forex
asset-type: OTC
typical-sessions:
  - "[[SES-TYPE-OTC]]"
behaviour-notes: ""
tags:
  - asset
  - reference
---

## Asset Profile

**Class:** Forex
**Type:** OTC

## Trading History

```dataview
TABLE date, time, direction, result, round(choice(result = "WIN", stake * (payout/100), choice(result = "LOSS", -stake, 0)), 2) as "P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND contains(asset, "EUR-USD-OTC")
SORT date DESC, time DESC
LIMIT 10
```
