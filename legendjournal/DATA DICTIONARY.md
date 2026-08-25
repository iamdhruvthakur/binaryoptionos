# DATA DICTIONARY

> Complete reference for all properties used in the Trading OS vault.

---

## UNIVERSAL PROPERTIES

Present on all structured notes.

| Property | Type | Description | Values |
|---|---|---|---|
| `note-type` | text | Identifies the note type | trade, session, review, strategy, strategy-version, strategy-changelog, research-experiment, backtest, observation, asset, market-regime, session-type, variable, mistake, psychology-observation, evidence, knowledge, system-config, dashboard |
| `id` | text | Unique identifier (same as filename without .md) | Pattern: PREFIX-YYYYMMDD-HHMMSS |
| `tags` | list | Note tags | Matches note-type value |

---

## TRADE PROPERTIES

| Property | Type | Description | Allowed Values |
|---|---|---|---|
| `trade-type` | text | Asset classification | FOREX, BINARY |
| `date` | date | Trade date | YYYY-MM-DD |
| `time` | text | Entry time (24h) | "HH:MM" |
| `day-of-week` | text | Day name | Monday, Tuesday, ... |
| `asset` | text | Asset traded (link to Asset note) | [[AST-...]] |
| `session` | text | Trading session (link to Session Type note) | [[SES-TYPE-...]] |
| `strategy` | text | Strategy (link to Strategy note) | [[STR-...]] |
| `strategy-version` | text | Version used (link to Version note) | [[VER-...]] |
| `setup` | text | Setup description | Free text |
| `direction` | text | Trade direction | CALL, PUT |
| `expiry` | text | Expiry duration | 1m, 2m, 3m, 5m, 10m, 15m, 30m, 1h |
| `market-regime` | text | Market regime (link to Regime note) | [[REG-...]] |
| `market-behavior` | text | Algorithmic OTC behavior | [[BEH-...]] |
| `variables` | list | Variables present (links to Variable notes) | [[VAR-...]] list |
| `result` | text | Trade outcome | WIN, LOSS, VOID, BREAK-EVEN |
| `payout` | number | Payout percentage | Integer 0-100 |
| `stake` | number | Stake amount | Number |
| `net-pl` | number | Calculated Net P/L | Number |
| `mistake` | text | Mistake made (link to Mistake note, optional) | [[MST-...]] or empty |
| `psychology-flag` | boolean | Psychology was a factor | true, false |
| `psychology-note` | text | Brief psychology note | Free text |
| `evidence` | list | Evidence notes | [[EVD-...]] list |
| `session-ref` | text | Parent session note | [[SES-...]] |
| `reviewed` | boolean | Included in a review | true, false |
| `review-ref` | text | Daily review note link | [[REV-D-...]] |

---

## SESSION PROPERTIES

| Property | Type | Description | Allowed Values |
|---|---|---|---|
| `date` | date | Session date | YYYY-MM-DD |
| `day-of-week` | text | Day name | Monday -- Sunday |
| `session-type` | text | Session type link | [[SES-TYPE-...]] |
| `market-regime` | text | Dominant regime | [[REG-...]] |
| `start-time` | text | Session start | "HH:MM" |
| `end-time` | text | Session end | "HH:MM" |
| `assets-traded` | list | Assets traded | [[AST-...]] list |
| `strategy-version` | text | Version used | [[VER-...]] |
| `total-trades` | number | Total trades count | Integer |
| `wins` | number | Win count | Integer |
| `losses` | number | Loss count | Integer |
| `voids` | number | Void count | Integer |
| `win-rate` | number | Win rate percentage | Number 0-100 |
| `net-result` | text | Overall outcome | Free text |
| `mental-state` | text | Pre-session psychology | Free text |
| `session-notes` | text | Session notes | Free text |
| `reviewed` | boolean | Included in daily review | true, false |
| `review-ref` | text | Review note link | [[REV-D-...]] |
| `trades` | list | Trade notes in this session | [[TRD-...]] list |
| `evidence` | list | Evidence notes | [[EVD-...]] list |

---

## REVIEW PROPERTIES (DAILY)

| Property | Type | Description | Allowed Values |
|---|---|---|---|
| `review-type` | text | Review type | Daily |
| `date` | date | Review date | YYYY-MM-DD |
| `day-of-week` | text | Day name | Monday -- Sunday |
| `session-refs` | list | Sessions reviewed | [[SES-...]] list |
| `trade-refs` | list | Trades reviewed | [[TRD-...]] list |
| `total-trades` | number | Total trades count | Integer |
| `wins` | number | Win count | Integer |
| `losses` | number | Loss count | Integer |
| `win-rate` | number | Win rate percentage | Number 0-100 |
| `psychology-rating` | number | Self-assessed psychology score | 1-5 |
| `what-went-well` | text | Positive notes | Free text |
| `what-to-improve` | text | Improvement notes | Free text |

---

## REVIEW PROPERTIES (WEEKLY)

| Property | Type | Description | Allowed Values |
|---|---|---|---|
| `review-type` | text | Review type | Weekly |
| `week-number` | text | ISO week number (quoted) | "01" -- "52" |
| `year` | text | Year (quoted) | "YYYY" |
| `daily-reviews` | list | Daily review links | [[REV-D-...]] list |
| `total-trades` | number | Total trades count | Integer |
| `wins` | number | Win count | Integer |
| `losses` | number | Loss count | Integer |
| `win-rate` | number | Win rate percentage | Number 0-100 |
| `strategy-version` | text | Primary version used | [[VER-...]] |

---

## STRATEGY PROPERTIES

| Property | Type | Description |
|---|---|---|
| `name` | text | Strategy name |
| `status` | text | Active, Development, Testing, Archived, Deprecated |
| `created` | date | Creation date |
| `current-version` | text | Link to current version |
| `versions` | list | All version links |
| `description` | text | Strategy description |
| `core-concept` | text | Core concept summary |
| `primary-assets` | list | Preferred assets |
| `primary-sessions` | list | Preferred sessions |
| `primary-regimes` | list | Preferred regimes |

---

## STRATEGY VERSION PROPERTIES

| Property | Type | Description |
|---|---|---|
| `strategy` | text | Parent strategy link [[STR-...]] |
| `version` | text | Version number |
| `status` | text | Active, Testing, Retired, Superseded |
| `superseded-by` | text | Next version link |
| `supersedes` | text | Previous version link |
| `variables` | list | Variables used |
| `changelog` | text | Changelog link |
| `backtest-count` | number | Number of backtests |
| `live-trade-count` | number | Number of live trades |
| `win-rate` | number | Win rate percentage |

---

## RESEARCH EXPERIMENT PROPERTIES

| Property | Type | Description | Values |
|---|---|---|---|
| `title` | text | Experiment title | Free text |
| `status` | text | Experiment status | Open, In Progress, Completed, Abandoned |
| `hypothesis` | text | The hypothesis being tested | Free text |
| `method` | text | Research methodology | Free text |
| `conclusion-type` | text | Conclusion classification | CONFIRMED, REFUTED, INCONCLUSIVE, PARTIAL |
| `sample-size` | number | Number of data points | Integer |
| `date-started` | date | Start date | YYYY-MM-DD |
| `date-completed` | date | Completion date | YYYY-MM-DD |

---

## KNOWLEDGE NOTE PROPERTIES

| Property | Type | Description | Values |
|---|---|---|---|
| `title` | text | Note title | Free text |
| `information-type` | text | Knowledge classification | FACT, RULE, HYPOTHESIS, OBSERVATION, EXPERIMENT, CONCLUSION, PERSONAL-OPINION, UNVERIFIED-IDEA |
| `source` | text | Knowledge origin | OneNote, Personal Research, External, Unknown |
| `topic` | text | Subject area | Free text |
| `strategy-relevance` | list | Related strategies | [[STR-...]] list |
| `variable-relevance` | list | Related variables | [[VAR-...]] list |
| `status` | text | Currency status | Current, Superseded, Unverified, Archived |
| `migrated-from` | text | OneNote source reference | Free text |

---

## ADDITIONAL NOTE TYPE PROPERTIES

### Backtest
| Property | Type | Description |
|---|---|---|
| `date-run` | date | Backtest date |
| `asset` | text | Asset tested [[AST-...]] |
| `market-regime` | text | Regime tested [[REG-...]] |
| `date-range-start` | text | Start of data range |
| `date-range-end` | text | End of data range |

### Observation
| Property | Type | Description |
|---|---|---|
| `observation-type` | text | Market, Candle, Session, Asset, Variable, System |
| `information-type` | text | OBSERVATION, FACT, HYPOTHESIS, UNVERIFIED-IDEA |
| `summary` | text | Brief observation summary |

### Mistake
| Property | Type | Description |
|---|---|---|
| `name` | text | Mistake name |
| `category` | text | Execution, Psychology, Analysis, Risk, Timing |
| `frequency` | number | Occurrence count |
| `resolution` | text | How to prevent |
| `status` | text | Open, Resolved, Recurring, Monitoring |

### Psychology Observation
| Property | Type | Description |
|---|---|---|
| `bias-type` | text | FOMO, Revenge, Overconfidence, Fear, Tilt, Hesitation, None |
| `impact` | text | Negative, Positive, Neutral |
| `emotional-state` | text | Description of state |

### Evidence
| Property | Type | Description |
|---|---|---|
| `evidence-type` | text | Screenshot, Chart, Annotation, Video, Document |
| `trade-ref` | text | Linked trade [[TRD-...]] |

### Asset
| Property | Type | Description |
|---|---|---|
| `name` | text | Display name (e.g. EUR/USD) |
| `alias` | text | System alias (e.g. EUR-USD) |
| `asset-class` | text | Forex, Crypto, Commodity, Index, Stock |
| `asset-type` | text | Live, OTC |

### Variable
| Property | Type | Description |
|---|---|---|
| `name` | text | Full variable name |
| `alias` | text | Short alias |
| `category` | text | Primary, Secondary, Confluence, Event, Filter |

### Strategy Changelog
| Property | Type | Description |
|---|---|---|
| `from-version` | text | Previous version [[VER-...]] |
| `to-version` | text | New version [[VER-...]] |
| `change-type` | text | Addition, Removal, Modification, Restructure |

---

## CONTROLLED VOCABULARY REFERENCE

### Result
`WIN` `LOSS` `VOID` `BREAK-EVEN`

### Direction
`CALL` `PUT`

### Market Regime
`Normal` `Reversal` `Choppy` `Trending`

### Session
`London` `New York` `Asian` `London-NY Overlap` `Pre-Market` `Post-Market`

### Strategy Status
`Active` `Development` `Testing` `Archived` `Deprecated`

### Strategy Version Status
`Active` `Testing` `Retired` `Superseded`

### Research Status
`Open` `In Progress` `Completed` `Abandoned`

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
`FOREX` `BINARY`

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
*[[SYSTEM GUIDE|System Guide]]* | *[[WORKFLOW GUIDE|Workflow Guide]]* | *[[Dashboard - Trading OS|Home]]*