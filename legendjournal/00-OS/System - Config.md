---
note-type: system-config
title: "Trading OS — System Configuration"
last-updated: 2026-08-24
current-strategy: "[[STR-V6]]"
current-version: "[[VER-V6.2]]"
system-status: Active
tags:
  - system
  - config
---

# Trading OS — System Configuration

> This note documents controlled vocabularies, system settings, and configuration for the Trading OS.
> Update this when adding new assets, variables, or changing controlled values.

---

## Current System State

| Setting | Value |
|---|---|
| Current Strategy | [[STR-V6]] |
| Current Version | [[VER-V6.2]] |
| System Status | Active |

---

## Controlled Vocabularies

### Result Values
`WIN` `LOSS` `VOID` `BREAK-EVEN`

### Direction Values
`CALL` `PUT`

### Market Regime Values
`Normal` `Reversal` `Choppy` `Trending`

### Session Values
`London` `New York` `Asian` `London-NY Overlap` `Pre-Market` `Post-Market`

### Strategy Status
`Active` `Development` `Testing` `Archived` `Deprecated`

### Strategy Version Status
`Active` `Testing` `Retired` `Superseded`

### Research Status
`Open` `In Progress` `Completed` `Abandoned`

### Conclusion Type
`CONFIRMED` `REFUTED` `INCONCLUSIVE` `PARTIAL`

### Information Type
`FACT` `RULE` `HYPOTHESIS` `OBSERVATION` `EXPERIMENT` `CONCLUSION` `PERSONAL-OPINION` `UNVERIFIED-IDEA`

### Mistake Category
`Execution` `Psychology` `Analysis` `Risk` `Timing`

### Mistake Status
`Open` `Resolved` `Recurring` `Monitoring`

### Variable Category
`Primary` `Secondary` `Confluence` `Event` `Filter`

### Expiry Values
`1m` `2m` `3m` `5m` `10m` `15m` `30m` `1h`

### Asset Class
`Forex` `Crypto` `Commodity` `Index` `Stock`

### Asset Type
`Live` `OTC`

### Trade Type
`BINARY`

### Market Behavior
`NORMAL` `REVERSAL` `UNKNOWN`

### Bias Type
`FOMO` `Revenge` `Overconfidence` `Fear` `Tilt` `Hesitation` `None`

### Evidence Type
`Screenshot` `Chart` `Annotation` `Video` `Document`

### Change Type
`Addition` `Removal` `Modification` `Restructure`

### Observation Type
`Market` `Candle` `Session` `Asset` `Variable` `System`

### Impact
`Negative` `Positive` `Neutral`

### Review Type
`Daily` `Weekly`

### Strategy Suitability
`High` `Medium` `Low`

---

## Registered Assets

> Add asset links here when new assets are created.

---

## Registered Variables

- [[VAR-SNR]] — Support & Resistance
- [[VAR-Short]] — Short Variable
- [[VAR-Sub]] — Sub Variable
- [[VAR-Events]] — Events Variable
- [[VAR-Acceleration]] — Acceleration Variable
- [[VAR-Line-Confluence]] — Line / Confluence Variable

---

## Registered Market Regimes

- [[REG-Normal]] — Normal
- [[REG-Reversal]] — Reversal
- [[REG-Choppy]] — Choppy
- [[REG-Trending]] — Trending

---

## Registered Market Behaviors

- [[BEH-NORMAL]] — NORMAL (OTC)
- [[BEH-REVERSAL]] — REVERSAL (OTC)
- [[BEH-UNKNOWN]] — UNKNOWN (OTC)

---

## Registered Session Types

- [[SES-TYPE-London]] — London (UTC 08:00-17:00)
- [[SES-TYPE-New-York]] — New York (UTC 13:00-22:00)
- [[SES-TYPE-Asian]] — Asian (UTC 00:00-09:00)
- [[SES-TYPE-London-NY-Overlap]] — London-NY Overlap (UTC 13:00-17:00)
- [[SES-TYPE-Pre-Market]] — Pre-Market
- [[SES-TYPE-Post-Market]] — Post-Market

---
*[[Dashboard - Trading OS|Home]]*