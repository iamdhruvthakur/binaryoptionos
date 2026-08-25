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

<div class="tos-subtitle">Regimes · Sessions · Assets · Behavior Classification</div>

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

## MARKET REGIMES

| Regime | Suitability | Description |
|---|---|---|
| [[REG-Normal\|Normal]] | High | Regular momentum, clear structure |
| [[REG-Reversal\|Reversal]] | High | Active counter-trend move |
| [[REG-Choppy\|Choppy]] | Low | No clear direction, false breakouts |
| [[REG-Trending\|Trending]] | Medium | Sustained directional move |

### Regime Performance

```dataview
TABLE WITHOUT ID
  market-regime as "Regime",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY market-regime
SORT length(rows) DESC
```

> *No trade data available for regime analysis.*

---

## MARKET BEHAVIORS (OTC)

| Behavior | Description |
|---|---|
| [[BEH-NORMAL\|NORMAL]] | Standard algorithmic execution |
| [[BEH-REVERSAL\|REVERSAL]] | Counter-directional algorithm active |
| [[BEH-UNKNOWN\|UNKNOWN]] | Unclassified or ambiguous behavior |

### Behavior Performance

```dataview
TABLE WITHOUT ID
  market-behavior as "Behavior",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY market-behavior
SORT length(rows) DESC
```

> *No behavior data available.*

---

## SESSION TYPES

| Session | UTC Window | IST Window |
|---|---|---|
| [[SES-TYPE-Pre-Market\|Pre-Market]] | Before open | Preparation |
| [[SES-TYPE-London\|London]] | 08:00 – 17:00 | 13:30 – 22:30 |
| [[SES-TYPE-London-NY-Overlap\|Overlap]] | 13:00 – 17:00 | 18:30 – 22:30 |
| [[SES-TYPE-New-York\|New York]] | 13:00 – 22:00 | 18:30 – 03:30 |
| [[SES-TYPE-Asian\|Asian]] | 00:00 – 09:00 | 05:30 – 14:30 |
| [[SES-TYPE-Post-Market\|Post-Market]] | After close | Review |

### Session Performance

```dataview
TABLE WITHOUT ID
  session as "Session",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY session
SORT length(rows) DESC
```

> *No session performance data available.*

---

## ASSET TYPE PERFORMANCE (LIVE vs OTC)

```dataview
TABLE WITHOUT ID
  asset-type as "Asset Type",
  length(rows) as "Trades",
  length(filter(rows, (r) => r.result = "WIN")) as "W",
  length(filter(rows, (r) => r.result = "LOSS")) as "L",
  round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"
FROM "01-Journal/Trades"
WHERE note-type = "trade"
GROUP BY asset-type
SORT length(rows) DESC
```

> *No asset type performance data available.*

---

## REGISTERED ASSETS

```dataview
TABLE name, asset-class, asset-type, typical-sessions
FROM "04-Market/Assets"
WHERE note-type = "asset"
SORT asset-class ASC
```

> *No assets registered. Use **+ NEW ASSET** to add one.*

---

## RECENT MARKET OBSERVATIONS

```dataview
TABLE date, observation-type, summary, status
FROM "03-Research/Observations"
WHERE note-type = "observation" AND (observation-type = "Market" OR observation-type = "Asset" OR observation-type = "Session")
SORT date DESC
LIMIT 10
```

> *No market observations recorded.*

---
*[[Dashboard - Trading OS|Home]] · [[Dashboard - Trading|Trading]] · [[_Bases/Assets.base|Assets Database]]*
