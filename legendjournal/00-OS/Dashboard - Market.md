---
note-type: dashboard
title: Market Dashboard
cssclasses:
  - dashboard
tags:
  - dashboard
---

<div class="tos-nav">
  [[Dashboard - Trading OS|HOME]]
  [[Dashboard - Trading|TRADING]]
  [[Dashboard - Strategy|STRATEGY]]
  [[Dashboard - Research|RESEARCH]]
  <strong>MARKET</strong>
  [[Dashboard - Psychology|PSYCHOLOGY]]
  [[Dashboard - Review|REVIEW]]
  [[Dashboard - Knowledge|KNOWLEDGE]]
</div>

# MARKET

<div class="tos-subtitle">Quotex Asset Registry · Regimes · Behaviors</div>

<div class="quick-actions">

```meta-bind-button
style: default
label: "+ NEW ASSET"
id: btn-new-asset
actions:
  - type: command
    command: quickadd:choice:14-new-asset
```

```meta-bind-button
style: default
label: "+ OBSERVATION"
id: btn-mkt-obs
actions:
  - type: command
    command: quickadd:choice:10-new-observation
```

</div>

---

## MARKET REGIMES (Structural)

| Regime | Suitability | Description |
|---|---|---|
| [[REG-Normal\|Normal]] | High | Regular momentum, clear structure |
| [[REG-Reversal\|Reversal]] | High | Active counter-trend move |
| [[REG-Choppy\|Choppy]] | Low | No clear direction, false breakouts |
| [[REG-Trending\|Trending]] | Medium | Sustained directional move |

---

## MARKET BEHAVIORS (OTC Algorithms)

```dataview
TABLE WITHOUT ID
  market-behavior as "Behavior",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY market-behavior
SORT length(rows) DESC
```

> *No behavior data available.*

---

## REGISTERED ASSETS

```dataview
TABLE name, asset-class, asset-type
FROM "04-Market/Assets"
WHERE note-type = "asset"
SORT asset-type DESC, asset-class ASC
```

> *No assets registered.*

---

## ASSET PERFORMANCE

```dataview
TABLE WITHOUT ID
  asset as "Asset",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate",
  round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"
FROM "01-Journal/Trades"
WHERE note-type = "trade" AND trade-type != "FOREX"
GROUP BY asset
SORT length(rows) DESC
```

> *No live trade data for assets.*

---

## ASSET OBSERVATIONS

```dataview
TABLE date, summary, information-type
FROM "03-Research/Observations"
WHERE note-type = "observation" AND observation-type = "Asset"
SORT date DESC
LIMIT 5
```

> *No recent asset observations.*

---
*[[Dashboard - Trading OS|Home]] · [[_Bases/Assets.base|Assets Database]]*
