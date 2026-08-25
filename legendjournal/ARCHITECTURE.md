# ARCHITECTURE.md
## Binary Options Trading Research & Knowledge Operating System
### Phase 1 â€” System Architecture Document

**Vault:** legendjournal
**Date:** 2026-08-24
**Status:** AWAITING USER APPROVAL â€” Do not implement until approved

---

## TABLE OF CONTENTS

1. Audit Results
2. System Objective
3. Design Principles
4. Absolute Constraints
5. Plugin Strategy
6. Folder Architecture
7. Entity Model
8. Property Schema
9. Controlled Vocabularies
10. Naming Conventions
11. Relationship Model
12. Template Architecture
13. Dashboard Architecture
14. Automation Architecture
15. Calculation Responsibility Matrix
16. Data Standards
17. Mobile Compatibility Rules
18. OneNote Migration Strategy
19. Scalability Design
20. Known Risks
21. Assumptions
22. Decisions Made
23. Decisions Intentionally Deferred
24. Phase 2 Scope

---

## 1. AUDIT RESULTS

### Vault State

| Item | Status |
|---|---|
| Vault name | legendjournal |
| Existing content notes | 1 (Welcome.md â€” default Obsidian stub, safe to delete) |
| Existing folder structure | None |
| Existing templates | None |
| Existing dashboards | None |
| Existing data | None |
| Migration risk | Zero â€” clean slate |

### Installed Community Plugins

| Plugin | Version | Mobile Compatible | Decision |
|---|---|---|---|
| Dataview | 0.5.68 | Yes | KEEP |
| Templater | 2.25.0 | Yes | KEEP |
| QuickAdd | 2.22.0 | Yes | KEEP |
| Meta Bind | 1.5.1 | Yes | KEEP |
| Calendar | 1.5.10 | Yes | KEEP (navigational only) |

### Enabled Native Core Plugins

| Plugin | Relevance |
|---|---|
| Bases | PRIMARY database view engine (enabled) |
| Properties | Required for all metadata (enabled) |
| Daily Notes | Used for Daily Review system (enabled) |
| Sync | Cross-device sync confirmed (enabled) |
| Canvas | Available for visual strategy maps (enabled) |
| Backlinks, Graph, Bookmarks, Search | Navigation tools (enabled) |

### Conflicts Identified

None. Clean vault with no existing structure to conflict with.

---

## 2. SYSTEM OBJECTIVE

This vault is the permanent **Binary Options Trading Research & Knowledge Operating System (Trading OS)**. It must function simultaneously as:

1. A trading knowledge base
2. A strategy repository
3. A strategy-development laboratory
4. A trading journal
5. A session journal
6. A backtesting/research repository
7. A market-behaviour research system
8. A trading psychology/mistake database
9. A structured evidence repository
10. A personal trading operating system
11. A searchable database
12. A visual analytics/dashboard environment

The system must remain useful at thousands of notes, work across all devices without modification, and evolve without destroying existing information.

---

## 3. DESIGN PRINCIPLES

**P1 â€” Properties Over Folders**
Folders provide filing. Properties provide meaning. Every important attribute is a property, enabling cross-folder queries.

**P2 â€” Links Provide Relationships**
Notes reference each other through wiki-links. The graph view should reveal the structure of the trading system.

**P3 â€” Templates Are the Only Entry Point**
Structured notes are ONLY created through QuickAdd + Templater. No structured note is ever created as a blank file.

**P4 â€” Controlled Vocabularies Everywhere**
All categorical properties use a fixed approved vocabulary enforced by Meta Bind dropdowns.

**P5 â€” Mobile-First, Desktop-Enhanced**
Every workflow works on mobile. Desktop-only features are never the sole path to a critical action.

**P6 â€” Evidence Is a First-Class Entity**
Screenshots are their own note type with properties and links, not file attachments.

**P7 â€” Information Type Integrity**
The system distinguishes: FACT / RULE / HYPOTHESIS / OBSERVATION / EXPERIMENT / CONCLUSION / PERSONAL-OPINION / UNVERIFIED-IDEA. This distinction survives migration permanently.

**P8 â€” Scalability by Design**
No component degrades at 1000+ notes. Queries are folder-scoped. Date-keyed subfolders prevent directory bloat.

**P9 â€” Minimum Plugin Surface**
Fewer plugins = fewer maintenance risks. Every plugin must justify its presence.

**P10 â€” The System Must Be Legible**
Folder names, file names, and templates are self-explanatory without consulting this document.

---

## 4. ABSOLUTE CONSTRAINTS

| Constraint | Status |
|---|---|
| No Python | Enforced â€” no .py files anywhere |
| No external database | Enforced â€” all data in Obsidian notes |
| No external backend or server | Enforced |
| No shell scripts in critical workflows | Enforced |
| No laptop dependency | Enforced â€” Obsidian Sync handles cross-device |
| No desktop-only plugins in critical paths | Enforced â€” all plugins verified mobile-compatible |
| All calculations inside vault | Enforced â€” Dataview, Bases, Templater only |

---

## 5. PLUGIN STRATEGY

### Retained Plugins and Their Responsibilities

#### Native Core: Bases
Primary database view engine.
- Trade database views (filterable by asset, strategy, result, regime)
- Session, Strategy, Backtest, Research, Mistake databases
- All persistent table-based views the user navigates regularly
- Mobile: native, fully compatible

#### Community: Dataview
Query engine for computed statistics and dynamic lists.
- Performance statistics: win rate, trade counts, rolling averages
- Variable performance analysis
- Filtered lists (open experiments, unreviewed sessions, recent mistakes)
- DataviewJS used ONLY when plain DQL is insufficient
- Mobile: compatible

#### Community: Templater
Note creation automation engine.
- All structured note templates with auto-populated date, time, ID properties
- Folder routing (creates notes in correct subfolder automatically)
- User prompts for key properties at creation time (max 3 per template for mobile performance)
- Mobile: compatible

#### Community: QuickAdd
Unified entry point for all note creation.
- One QuickAdd command per note type
- All macros are Template type â€” never Capture type
- Available in command palette on all platforms
- Mobile: compatible

#### Community: Meta Bind
Interactive UI layer within notes.
- Dropdown selectors for result, market regime, session, status values
- Toggle buttons for boolean properties (reviewed, psychology-flag)
- Action buttons on dashboards triggering QuickAdd commands
- Updates note frontmatter directly â€” controlled-vocabulary enforcement mechanism
- Mobile: compatible

#### Community: Calendar
Sidebar date navigation.
- Visual navigation to Daily Review and Session notes by date
- Not in any critical data path â€” system fully functional without it
- Mobile: compatible

---

### Plugins Considered and Rejected

| Plugin | Reason Rejected |
|---|---|
| DB Folder | Superseded by native Bases |
| Tasks | Trade/research statuses are properties, not task-list items. Wrong data model. |
| Obsidian Charts | Cosmetic only. Dataview tables sufficient for core analytics. |
| Kanban | Canvas (native) available if visual boards needed. |
| Periodic Notes | Covered by Daily Notes (native) + Templater. |
| Excalidraw | Canvas (native) sufficient. Adds mobile performance overhead. |
| BRAT | Development tool only â€” not appropriate in production vault. |

---

## 6. FOLDER ARCHITECTURE

Folders are maximum 3 levels deep for mobile navigability. Numeric prefixes enforce consistent sort order. Underscore prefixes group system folders at the bottom of the explorer.

`
legendjournal/
|
+-- 00-OS/                            OS layer: dashboards and config
|   +-- Dashboard - Trading OS.md     Home screen / master dashboard
|   +-- Dashboard - Trading.md
|   +-- Dashboard - Strategy.md
|   +-- Dashboard - Research.md
|   +-- Dashboard - Psychology.md
|   +-- Dashboard - Review.md
|   +-- System - Config.md            Controlled vocabulary reference
|
+-- 01-Journal/                       Live trading records
|   +-- Sessions/
|   |   +-- YYYY/                     Year subfolder for scalability
|   +-- Trades/
|   |   +-- YYYY/
|   +-- Reviews/
|       +-- YYYY/
|
+-- 02-Strategies/                    Strategy knowledge system
|   +-- Registry/                     One note per strategy (master record)
|   +-- Versions/                     One note per version
|   +-- Changelogs/                   Strategy change history
|
+-- 03-Research/                      Research laboratory
|   +-- Experiments/
|   +-- Backtests/
|   +-- Observations/
|
+-- 04-Market/                        Market reference notes
|   +-- Assets/                       One note per tradable instrument
|   +-- Regimes/                      One note per market regime type
|   +-- Sessions/                     One note per session type
|
+-- 05-Variables/                     Variable system (one note per variable)
|
+-- 06-Psychology/                    Psychology and mistakes
|   +-- Mistakes/                     One note per mistake category
|   +-- Observations/
|
+-- 07-Knowledge/                     General knowledge base
|   +-- Concepts/                     Atomic concept notes
|   +-- Rules/                        Trading rules (clearly marked RULE)
|   +-- Imported/                     OneNote migration staging area
|
+-- 08-Evidence/                      Evidence and screenshots
|
+-- _Templates/                       All Templater templates
|   +-- TPL-Trade.md
|   +-- TPL-Session.md
|   +-- TPL-Strategy.md
|   +-- TPL-StrategyVersion.md
|   +-- TPL-Changelog.md
|   +-- TPL-Backtest.md
|   +-- TPL-Research.md
|   +-- TPL-Observation.md
|   +-- TPL-Mistake.md
|   +-- TPL-Psychology.md
|   +-- TPL-Evidence.md
|   +-- TPL-DailyReview.md
|   +-- TPL-WeeklyReview.md
|   +-- TPL-Asset.md
|   +-- TPL-Variable.md
|   +-- TPL-KnowledgeNote.md
|
+-- _Bases/                           Obsidian Bases database files
    +-- Trades.base
    +-- Sessions.base
    +-- Strategies.base
    +-- Backtests.base
    +-- Research.base
    +-- Mistakes.base
    +-- Variables.base
`

---

## 7. ENTITY MODEL

18 distinct note types. Types have been combined where a separate schema added no value.

| # | Entity | Folder | One Note Per |
|---|---|---|---|
| 1 | Trade | 01-Journal/Trades/YYYY/ | Each individual trade |
| 2 | Session | 01-Journal/Sessions/YYYY/ | Each trading session |
| 3 | Daily Review | 01-Journal/Reviews/YYYY/ | Each calendar day |
| 4 | Weekly Review | 01-Journal/Reviews/YYYY/ | Each calendar week |
| 5 | Strategy | 02-Strategies/Registry/ | Each strategy (master record) |
| 6 | Strategy Version | 02-Strategies/Versions/ | Each numbered version |
| 7 | Strategy Changelog | 02-Strategies/Changelogs/ | Each documented change event |
| 8 | Research Experiment | 03-Research/Experiments/ | Each formal experiment |
| 9 | Backtest | 03-Research/Backtests/ | Each backtest run |
| 10 | Market Observation | 03-Research/Observations/ | Each recorded observation |
| 11 | Asset | 04-Market/Assets/ | Each tradable instrument |
| 12 | Market Regime | 04-Market/Regimes/ | Each regime type (reference) |
| 13 | Session Type | 04-Market/Sessions/ | Each session type (reference) |
| 14 | Variable | 05-Variables/ | Each variable in the system |
| 15 | Mistake | 06-Psychology/Mistakes/ | Each mistake category |
| 16 | Psychology Observation | 06-Psychology/Observations/ | Each qualitative psychology note |
| 17 | Knowledge Note | 07-Knowledge/ | Each atomic concept or rule |
| 18 | Evidence | 08-Evidence/ | Each screenshot or chart note |

**Key combination decisions:**
- Mistake = categorical (recurring pattern, queryable). Psychology Observation = qualitative diary. Kept separate.
- Daily Review and Weekly Review share note-type: review, differentiated by review-type property.
- Strategy Changelog is a separate entity â€” must be independently queryable without modifying the version note.

---

## 8. PROPERTY SCHEMA

All properties use YAML frontmatter. Keys: kebab-case. Dates: YYYY-MM-DD. Times: "HH:MM" (24h, quoted). Arrays: YAML list format.

### 8.1 Trade

`yaml
---
note-type: trade
id: TRD-20260824-001
date: 2026-08-24
time: "09:32"
asset: "[[AST-EUR-USD]]"
session: "[[SES-TYPE-London]]"
strategy: "[[STR-V6]]"
strategy-version: "[[VER-V6.2]]"
setup: ""
direction: CALL
expiry: "5m"
market-regime: "[[REG-Normal]]"
variables:
  - "[[VAR-SNR]]"
result: WIN
payout: 85
stake: 10
mistake: ""
psychology-flag: false
psychology-note: ""
evidence: []
session-ref: "[[SES-20260824-01]]"
reviewed: false
review-ref: ""
tags:
  - trade
---
`

### 8.2 Session

`yaml
---
note-type: session
id: SES-20260824-01
date: 2026-08-24
day-of-week: Monday
session-type: "[[SES-TYPE-London]]"
market-regime: "[[REG-Normal]]"
start-time: "08:00"
end-time: "11:00"
assets-traded: []
strategy-version: "[[VER-V6.2]]"
total-trades: 0
wins: 0
losses: 0
voids: 0
win-rate: 0
net-result: ""
mental-state: ""
session-notes: ""
reviewed: false
review-ref: ""
trades: []
evidence: []
tags:
  - session
---
`

### 8.3 Strategy (Master Record)

`yaml
---
note-type: strategy
id: STR-V6
name: "Strategy V6"
status: Active
created: 2026-08-24
current-version: "[[VER-V6.2]]"
versions: []
description: ""
core-concept: ""
primary-assets: []
primary-sessions: []
primary-regimes: []
tags:
  - strategy
---
`

### 8.4 Strategy Version

`yaml
---
note-type: strategy-version
id: VER-V6.2
strategy: "[[STR-V6]]"
version: "6.2"
status: Active
created: 2026-08-24
superseded-by: ""
supersedes: "[[VER-V6.1]]"
variables: []
changelog: "[[CL-V6.2]]"
backtest-count: 0
live-trade-count: 0
win-rate: 0
tags:
  - strategy-version
---
`

### 8.5 Strategy Changelog

`yaml
---
note-type: strategy-changelog
id: CL-V6.2
date: 2026-08-24
strategy: "[[STR-V6]]"
from-version: "[[VER-V6.1]]"
to-version: "[[VER-V6.2]]"
change-type: Modification
reason: ""
change-summary: ""
evidence: []
tags:
  - changelog
---
`

### 8.6 Research Experiment

`yaml
---
note-type: research-experiment
id: EXP-20260824-001
title: ""
date-started: 2026-08-24
date-completed: ""
status: Open
hypothesis: ""
method: ""
dataset-description: ""
strategy: "[[STR-V6]]"
strategy-version: "[[VER-V6.2]]"
variables: []
market-regimes: []
assets: []
sessions: []
sample-size: 0
result: ""
conclusion: ""
conclusion-type: ""
evidence: []
related-experiments: []
tags:
  - research
---
`

### 8.7 Backtest

`yaml
---
note-type: backtest
id: BT-20260824-001
date-run: 2026-08-24
strategy: "[[STR-V6]]"
strategy-version: "[[VER-V6.2]]"
asset: "[[AST-EUR-USD]]"
session: "[[SES-TYPE-London]]"
market-regime: "[[REG-Normal]]"
date-range-start: ""
date-range-end: ""
total-trades: 0
wins: 0
losses: 0
voids: 0
win-rate: 0
notes: ""
conclusion: ""
evidence: []
tags:
  - backtest
---
`

### 8.8 Market Observation

`yaml
---
note-type: observation
id: OBS-20260824-001
date: 2026-08-24
observation-type: Market
information-type: OBSERVATION
asset: []
session: []
market-regime: []
strategy: []
variables: []
summary: ""
evidence: []
status: Open
tags:
  - observation
---
`

### 8.9 Asset Reference

`yaml
---
note-type: asset
id: AST-EUR-USD
name: "EUR/USD"
alias: "EUR-USD"
asset-class: Forex
typical-sessions: []
behaviour-notes: ""
tags:
  - asset
---
`

### 8.10 Market Regime Reference

`yaml
---
note-type: market-regime
id: REG-Normal
name: Normal
description: ""
characteristics: ""
behaviour-notes: ""
tags:
  - market-regime
---
`

### 8.11 Session Type Reference

`yaml
---
note-type: session-type
id: SES-TYPE-London
name: London
utc-open: "08:00"
utc-close: "16:00"
typical-assets: []
behaviour-notes: ""
tags:
  - session-type
---
`

### 8.12 Variable Reference

`yaml
---
note-type: variable
id: VAR-SNR
name: "Support & Resistance"
alias: SNR
category: Primary
description: ""
rules: ""
strategy-versions: []
evidence: []
tags:
  - variable
---
`

### 8.13 Mistake Category

`yaml
---
note-type: mistake
id: MST-Early-Entry
name: ""
category: Execution
description: ""
frequency: 0
resolution: ""
status: Open
associated-strategies: []
associated-regimes: []
associated-sessions: []
associated-variables: []
tags:
  - mistake
---
`

### 8.14 Psychology Observation

`yaml
---
note-type: psychology-observation
id: PSY-20260824-001
date: 2026-08-24
session-ref: ""
trade-ref: ""
emotional-state: ""
bias-type: None
impact: Neutral
resolution: ""
tags:
  - psychology
---
`

### 8.15 Daily Review

`yaml
---
note-type: review
review-type: Daily
date: 2026-08-24
day-of-week: Monday
session-refs: []
trade-refs: []
total-trades: 0
wins: 0
losses: 0
win-rate: 0
key-observations: ""
mistakes-identified: []
psychology-rating: 3
what-went-well: ""
what-to-improve: ""
tags:
  - review
  - daily-review
---
`

### 8.16 Weekly Review

`yaml
---
note-type: review
review-type: Weekly
week-number: 34
year: 2026
date-start: 2026-08-19
date-end: 2026-08-24
daily-reviews: []
total-trades: 0
wins: 0
losses: 0
win-rate: 0
strategy-version: "[[VER-V6.2]]"
regime-summary: ""
key-discoveries: ""
strategy-adjustments: ""
goals-next-week: ""
tags:
  - review
  - weekly-review
---
`

### 8.17 Evidence

`yaml
---
note-type: evidence
id: EVD-20260824-001
date: 2026-08-24
evidence-type: Screenshot
asset: ""
session: ""
trade-ref: ""
strategy-version: ""
market-regime: ""
description: ""
tags:
  - evidence
---
`

### 8.18 Knowledge Note

`yaml
---
note-type: knowledge
id: KNW-Hammer-Candle
title: ""
information-type: CONCEPT
source: ""
topic: ""
strategy-relevance: []
variable-relevance: []
status: Current
migrated-from: ""
tags:
  - knowledge
---
`

---

## 9. CONTROLLED VOCABULARIES

These are the ONLY approved values for categorical properties. Meta Bind dropdowns enforce these at input time. Any additions must be documented here first.

**Result:** WIN | LOSS | VOID | BREAK-EVEN

**Direction:** CALL | PUT

**Market Regime:** Normal | Reversal | Choppy | Trending

**Session:** London | New York | Asian | London-NY Overlap | Pre-Market | Post-Market

**Strategy Status:** Active | Development | Testing | Archived | Deprecated

**Strategy Version Status:** Active | Testing | Retired | Superseded

**Research Status:** Open | In Progress | Completed | Abandoned

**Conclusion Type:** CONFIRMED | REFUTED | INCONCLUSIVE | PARTIAL

**Information Type:** FACT | RULE | HYPOTHESIS | OBSERVATION | EXPERIMENT | CONCLUSION | PERSONAL-OPINION | UNVERIFIED-IDEA

**Mistake Category:** Execution | Psychology | Analysis | Risk | Timing

**Mistake Status:** Open | Resolved | Recurring | Monitoring

**Variable Category:** Primary | Secondary | Confluence | Event | Filter

**Expiry:** 1m | 2m | 3m | 5m | 10m | 15m | 30m | 1h

**Asset Class:** Forex | Crypto | Commodity | Index | Stock

**Bias Type:** FOMO | Revenge | Overconfidence | Fear | Tilt | Hesitation | None

**Change Type:** Addition | Removal | Modification | Restructure

**Evidence Type:** Screenshot | Chart | Annotation | Video | Document

**Observation Type:** Market | Candle | Session | Asset | Variable | System

**Impact:** Negative | Positive | Neutral

---

## 10. NAMING CONVENTIONS

### File Naming Patterns

| Entity | Pattern | Example |
|---|---|---|
| Trade | TRD-YYYYMMDD-NNN | TRD-20260824-001.md |
| Session | SES-YYYYMMDD-NN | SES-20260824-01.md |
| Daily Review | REV-D-YYYY-MM-DD | REV-D-2026-08-24.md |
| Weekly Review | REV-W-YYYY-WNN | REV-W-2026-W34.md |
| Strategy | STR-[ShortName] | STR-V6.md |
| Strategy Version | VER-[Version] | VER-V6.2.md |
| Strategy Changelog | CL-[Version] | CL-V6.2.md |
| Research Experiment | EXP-YYYYMMDD-NNN | EXP-20260824-001.md |
| Backtest | BT-YYYYMMDD-NNN | BT-20260824-001.md |
| Observation | OBS-YYYYMMDD-NNN | OBS-20260824-001.md |
| Asset | AST-[ALIAS] | AST-EUR-USD.md |
| Market Regime | REG-[Name] | REG-Normal.md |
| Session Type | SES-TYPE-[Name] | SES-TYPE-London.md |
| Variable | VAR-[ShortName] | VAR-SNR.md |
| Mistake | MST-[ShortName] | MST-Early-Entry.md |
| Psychology Obs | PSY-YYYYMMDD-NNN | PSY-20260824-001.md |
| Evidence | EVD-YYYYMMDD-NNN | EVD-20260824-001.md |
| Knowledge Note | KNW-[ShortTitle] | KNW-Hammer-Candle.md |
| Template | TPL-[EntityType] | TPL-Trade.md |

### Rules
- No spaces in file names â€” use hyphens
- Asset names replace / with - (EUR/USD -> EUR-USD)
- File name = ID value (ID is the file name without .md)
- Property keys: kebab-case always
- Tags: lowercase-hyphenated always
- Internal links: [[FileName]] (wiki-links only, never raw markdown links for internal references)
- Multi-value properties: YAML list format (never comma-separated strings)

---

## 11. RELATIONSHIP MODEL

`
ASSET <------------------------------------------------------+
SESSION-TYPE <-----------------------------------------------+
MARKET-REGIME <----------------------------------------------+
VARIABLE <---------------------------------------------------+
                                                              |
STRATEGY ---------------------------------------------------->+
  +-- STRATEGY-VERSION ------------------------------------->+
        +-- STRATEGY-CHANGELOG                              |
        +-- BACKTEST ---------------------------------------->+
        +-- RESEARCH-EXPERIMENT ---------------------------->+
                                                              |
SESSION -------------------------------------------------------->+
  +-- TRADE -------------------------------------------------->+
        +-- EVIDENCE
        +-- MISTAKE (link to mistake category note)
        +-- PSYCHOLOGY-OBSERVATION

DAILY-REVIEW  -> references SESSION + TRADE
WEEKLY-REVIEW -> references DAILY-REVIEW

KNOWLEDGE-NOTE -> references STRATEGY, VARIABLE, OBSERVATION
OBSERVATION    -> references ASSET, SESSION-TYPE, MARKET-REGIME, VARIABLE
`

### Key Query Paths

| Question | Query Mechanism |
|---|---|
| Win rate by strategy version | Dataview: GROUP BY strategy-version on trades |
| Win rate by market regime | Dataview: GROUP BY market-regime on trades |
| Win rate by asset | Dataview: GROUP BY asset on trades |
| Win rate by session | Dataview: GROUP BY session on trades |
| Variable performance | Dataview: WHERE contains(variables, "[[VAR-X]]") |
| Variable combination performance | DataviewJS: filter trades containing both VAR-X AND VAR-Y |
| Mistake frequency | Dataview: GROUP BY mistake on trades |
| Open experiments | Bases/Dataview: WHERE status = Open or In Progress |
| Strategy version history | Bases: filter strategy-version notes by strategy link |
| Trades with psychology flag | Dataview: WHERE psychology-flag = true |

---

## 12. TEMPLATE ARCHITECTURE

### Template Design Rules
1. Every template begins with complete frontmatter (all properties pre-filled or Templater-generated)
2. Templates auto-generate id, date, time, day-of-week from Templater
3. Templates include body section headers for structured free-text content
4. Templates use tp.system.suggester() for max 3 critical properties (mobile performance)
5. Templates do NOT contain Dataview or DataviewJS blocks (those live in dashboards only)
6. Templates route to the correct subfolder via Templater tp.file.move()

### Template Inventory

| Template | Creates | QuickAdd Command |
|---|---|---|
| TPL-Trade.md | Trade note | New Trade |
| TPL-Session.md | Session note | New Session |
| TPL-DailyReview.md | Daily Review | Daily Review |
| TPL-WeeklyReview.md | Weekly Review | Weekly Review |
| TPL-Strategy.md | Strategy master | New Strategy |
| TPL-StrategyVersion.md | Strategy Version | New Strategy Version |
| TPL-Changelog.md | Changelog note | New Changelog |
| TPL-Research.md | Research Experiment | New Research Experiment |
| TPL-Backtest.md | Backtest | New Backtest |
| TPL-Observation.md | Market Observation | New Observation |
| TPL-Mistake.md | Mistake category | New Mistake |
| TPL-Psychology.md | Psychology note | New Psychology Note |
| TPL-Evidence.md | Evidence note | New Evidence |
| TPL-Asset.md | Asset reference | New Asset |
| TPL-Variable.md | Variable reference | New Variable |
| TPL-KnowledgeNote.md | Knowledge note | New Knowledge Note |

---

## 13. DASHBOARD ARCHITECTURE

### Dashboard Hierarchy

`
00-OS/
+-- Dashboard - Trading OS.md     Master home screen
+-- Dashboard - Trading.md        Trade data and performance
+-- Dashboard - Strategy.md       Strategy and version overview
+-- Dashboard - Research.md       Experiments and backtests
+-- Dashboard - Psychology.md     Mistakes and psychology
+-- Dashboard - Review.md         Reviews and calendar
`

### Dashboard - Trading OS (Home Screen)

Sections:
1. **System Status** â€” Current strategy and version (static wiki-links, manually updated)
2. **Quick Actions** â€” Meta Bind buttons: New Trade, New Session, Daily Review, New Observation
3. **Today at a Glance** â€” Dataview: today's sessions, today's trades
4. **Recent Sessions** â€” Dataview: last 7 sessions (LIMIT 7)
5. **Recent Trades** â€” Dataview: last 10 trades (LIMIT 10)
6. **Performance** â€” Dataview: rolling win rate 30d and 90d
7. **Open Research** â€” Dataview: experiments WHERE status = Open or In Progress
8. **Recent Mistakes** â€” Dataview: recent trades WHERE mistake != ""
9. **Navigation** â€” Wiki-links to all other dashboards and key system notes

### Dashboard - Trading
1. Trade database (Bases) â€” filterable by date, asset, regime, result, strategy
2. Performance statistics (Dataview) â€” win rate by regime, asset, session, variable
3. Mistake frequency table (Dataview)

### Dashboard - Strategy
1. Active strategy/version summary (static links)
2. All strategy versions (Bases)
3. All changelogs (Bases)
4. Backtest results by version (Dataview)
5. Live trade results by version (Dataview)

### Dashboard - Research
1. Open experiments (Dataview)
2. All experiments (Bases)
3. All backtests (Bases)
4. Recent observations (Dataview)
5. Confirmed conclusions (Dataview: WHERE status = Confirmed)

### Dashboard - Psychology
1. Mistake database (Bases)
2. Mistakes by frequency (Dataview sorted)
3. Psychology observations (Dataview)
4. Trades with psychology flag (Dataview)

### Dashboard - Review
1. Calendar sidebar navigation (Calendar plugin)
2. Recent daily reviews (Dataview)
3. Weekly reviews (Bases)
4. Sessions without linked review (Dataview â€” completion tracker)

---

## 14. AUTOMATION ARCHITECTURE

### QuickAdd Command Map

| Command | Template | Target Folder |
|---|---|---|
| New Trade | TPL-Trade.md | 01-Journal/Trades/YYYY/ |
| New Session | TPL-Session.md | 01-Journal/Sessions/YYYY/ |
| Daily Review | TPL-DailyReview.md | 01-Journal/Reviews/YYYY/ |
| Weekly Review | TPL-WeeklyReview.md | 01-Journal/Reviews/YYYY/ |
| New Strategy | TPL-Strategy.md | 02-Strategies/Registry/ |
| New Strategy Version | TPL-StrategyVersion.md | 02-Strategies/Versions/ |
| New Changelog | TPL-Changelog.md | 02-Strategies/Changelogs/ |
| New Research Experiment | TPL-Research.md | 03-Research/Experiments/ |
| New Backtest | TPL-Backtest.md | 03-Research/Backtests/ |
| New Observation | TPL-Observation.md | 03-Research/Observations/ |
| New Mistake | TPL-Mistake.md | 06-Psychology/Mistakes/ |
| New Psychology Note | TPL-Psychology.md | 06-Psychology/Observations/ |
| New Evidence | TPL-Evidence.md | 08-Evidence/ |
| New Knowledge Note | TPL-KnowledgeNote.md | 07-Knowledge/Concepts/ |

### Automation Principles
- Automation is limited to note creation and property pre-population only
- No automation silently modifies existing notes
- No background or scheduled automation
- User always sees what a template creates before it saves
- All QuickAdd macros are Template type (never Capture type)

---

## 15. CALCULATION RESPONSIBILITY MATRIX

| Calculation | Tool | Notes |
|---|---|---|
| Win rate (simple) | Dataview DQL | (wins / (wins + losses)) * 100 |
| Win rate by regime | Dataview DQL GROUP BY | Renders as table |
| Win rate by asset | Dataview DQL GROUP BY | Renders as table |
| Win rate by session | Dataview DQL GROUP BY | Renders as table |
| Win rate by variable | DataviewJS | contains() on array property |
| Variable combination performance | DataviewJS | Two-variable intersection filter |
| Trade count by session | Dataview DQL GROUP BY | Simple |
| Rolling 30d win rate | Dataview DQL | WHERE date >= date(today) - dur(30 days) |
| Mistake frequency | Dataview DQL | GROUP BY mistake |
| Experiment completion | Bases view | Filter by status column |
| Version comparison stats | Dataview DQL | Filter by strategy-version link |

**Technology Decision Summary:**
- Bases -> static database views (browsable, filterable by hand)
- Dataview DQL -> computed aggregations in dashboards
- DataviewJS -> complex array operations only (variable combinations)
- Templater -> calculations at note-creation time (ID, dates)
- Meta Bind -> UI input only (no calculations)

---

## 16. DATA STANDARDS

| Standard | Value |
|---|---|
| Date format | YYYY-MM-DD (ISO 8601) |
| Time format | "HH:MM" (24-hour, quoted YAML string) |
| Week number format | W34 (ISO week number) |
| Win rate | Integer 0-100 (not decimal fraction) |
| Payout | Integer percentage (e.g., 85) |
| Stake | Number in account currency (e.g., 10) |
| Booleans | true / false unquoted |
| Arrays | YAML list format â€” never comma-separated strings |
| Internal links | "[[FileName]]" in frontmatter, [[FileName]] in body |

---

## 17. MOBILE COMPATIBILITY RULES

### Hard Rules
1. Every critical workflow executable from Command Palette on mobile
2. No workflow requires right-click menus (unavailable on mobile)
3. No workflow requires mouse drag operations
4. No template requires operations outside Obsidian
5. All dashboard queries render without errors on mobile
6. All Bases views function on mobile (native feature)
7. DataviewJS queries use no Node.js-specific APIs

### Known Mobile Risks

| Risk | Severity | Mitigation |
|---|---|---|
| Templater suggester slow on older iOS | Medium | Max 3 prompts per template |
| DataviewJS complex queries lag on mobile | Medium | DQL preferred; JS used sparingly |
| Long Dataview tables scroll poorly on mobile | Medium | LIMIT 20 on all dashboard queries |
| Canvas limited on mobile | Low | Canvas is supplementary only |

### Mobile Verification Checklist (Phase 2)
- [ ] New Trade via command palette on iOS
- [ ] New Session via command palette on iOS
- [ ] Daily Review via command palette on iOS
- [ ] Editing trade note on iOS
- [ ] Meta Bind dropdown update on iOS
- [ ] Trading OS dashboard renders on iOS
- [ ] Bases database view renders on iOS
- [ ] Dataview win rate query renders on iOS

---

## 18. ONENOTE MIGRATION STRATEGY

### Principles
1. Never dump raw OneNote content into folders without classification
2. Every migrated note gets information-type and migrated-from properties
3. Raw imports land in 07-Knowledge/Imported/ first, then are classified
4. Trading rules are preserved in exact language â€” no paraphrasing
5. The distinction between FACT / RULE / HYPOTHESIS / OBSERVATION / EXPERIMENT / CONCLUSION / PERSONAL-OPINION / UNVERIFIED-IDEA is applied during classification, not during import

### Migration Workflow

`
Step 1: Export OneNote -> Markdown or HTML
Step 2: Place raw files in 07-Knowledge/Imported/
Step 3: Review each file, assign information-type property
Step 4: Split multi-concept pages into atomic knowledge notes where appropriate
Step 5: Link to relevant strategy, variable, and research notes
Step 6: Move classified notes to their permanent folder
Step 7: Archive or delete the raw import file
`

### Classification Map

| OneNote Content | System Destination | Note Type + Information Type |
|---|---|---|
| Trading rules | 07-Knowledge/Rules/ | knowledge + RULE |
| Observations | 03-Research/Observations/ | observation + OBSERVATION |
| Strategy descriptions | 02-Strategies/Registry/ or Versions/ | strategy or strategy-version |
| Variable descriptions | 05-Variables/ | variable |
| Hypotheses | 03-Research/Experiments/ | research-experiment |
| General concepts | 07-Knowledge/Concepts/ | knowledge + CONCEPT |
| Personal opinions | 07-Knowledge/Concepts/ | knowledge + PERSONAL-OPINION |
| Unverified ideas | 07-Knowledge/Concepts/ | knowledge + UNVERIFIED-IDEA |
| Historical trades | 01-Journal/Trades/YYYY/ | trade + migrated-from |
| Historical sessions | 01-Journal/Sessions/YYYY/ | session + migrated-from |

---

## 19. SCALABILITY DESIGN

### Year Subfolder Strategy
High-volume folders use YYYY/ subfolders:
- 01-Journal/Trades/2026/ â€” 200-1000+ files/year
- 01-Journal/Sessions/2026/ â€” 100-300 files/year
- 01-Journal/Reviews/2026/ â€” ~417 files/year

### Query Scope Strategy
All Dataview queries use folder-scoped FROM:
- CORRECT: FROM "01-Journal/Trades"
- AVOID: FROM #trade (vault-wide, slow at scale)

### Long-term Archive Strategy (Phase 4+)
After 3+ years: create _Archive/YYYY/ folders for old records. Dashboard queries limit to last 2 years by default with separate historical view available.

### Knowledge Note Atomicity
One concept per note. Multi-concept OneNote pages split into multiple atomic notes during migration.

---

## 20. KNOWN RISKS

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| DataviewJS required for variable combination analysis; complex to author on mobile | High | Medium | JS queries authored on desktop, render correctly on mobile |
| Templater ID generation not atomic across devices (concurrent creation = potential duplicate ID) | Medium | Low | IDs include date+sequence; duplicates detectable and manually fixable; IDs are informational not primary keys |
| Meta Bind 1.5.1 dropdown syntax must be verified against installed version | Low | High | Test all Meta Bind widgets before deploying templates in Phase 2 |
| Calendar plugin unmaintained; may break on Obsidian update | Medium | Low | Navigation only â€” system fully functional without it |
| Bases API may change in future Obsidian updates | Medium | Medium | Source data lives in note properties (safe); .base files can be recreated |
| OneNote export quality poor (images, tables, formatting) | High | Medium | Manual review required; no automated migration trusted |
| Large Dataview queries lag on mobile | Medium | Medium | LIMIT clauses, folder scoping, prefer Bases for static views |

---

## 21. ASSUMPTIONS

| # | Assumption | Basis |
|---|---|---|
| A1 | Binary options = fixed-expiry CALL/PUT with fixed payout percentage | Requirements mention payout, expiry, direction |
| A2 | Market regimes: Normal, Reversal, Choppy, Trending | Requirements name Normal and Reversal; Choppy and Trending are standard additions |
| A3 | Sessions: London, New York, Asian, London-NY Overlap | Standard Forex session framework |
| A4 | V6 is the current active strategy framework | Requirements describe V6 Variable System as the existing framework |
| A5 | Win rate = (wins / (wins + losses)) x 100, excluding VOIDs and BREAK-EVENs from denominator | Standard binary options convention |
| A6 | Stake amounts stored as numbers without currency label | Currency to be specified by user and added in Phase 2 |
| A7 | DataviewJS is enabled in Dataview settings | Required for variable combination queries |
| A8 | Short Variable, Sub Variable, Acceleration Variable, Events, Line/Confluence Variable are all instances of the variable entity type, not separate entity types | Unified model is simpler and fully queryable |
| A9 | Evidence notes are Obsidian notes with embedded images (not raw image files) | Enables properties and queries on evidence |
| A10 | Obsidian Sync is the cross-device sync mechanism | sync: true confirmed in core-plugins.json |
| A11 | Vault folder name legendjournal is intentional and will not be changed | Already created and named |
| A12 | Calendar plugin is retained for navigational convenience | No conflicts; mobile compatible; zero risk |

---

## 22. DECISIONS MADE

| Decision | Rationale |
|---|---|
| Bases is primary database view engine | Native, no-code, mobile-compatible, Obsidian's forward direction |
| Dataview DQL for aggregations, DataviewJS sparingly | DQL readable and maintainable; JS only where DQL insufficient |
| Unified note-type property on all entities | Enables cross-folder type-based queries |
| Year subfolders for high-volume entity types | Prevents directory bloat at thousands of notes |
| Date-keyed string IDs | Unique across devices without coordination mechanism |
| Evidence notes are full Obsidian notes with embedded images | Enables properties, links, queries on evidence |
| Strategy and Strategy Version are separate entities | Versions independently queryable with distinct performance metrics |
| Mistake notes are categorical (one per mistake type) | Mistakes are recurring patterns; occurrences recorded in Trade notes |
| Psychology Observations separate from Mistakes | Qualitative diary vs. categorical database â€” different query needs |
| Daily/Weekly Review share note-type: review with review-type discriminator | Reduces note types while maintaining separate views |
| information-type vocabulary applied to Knowledge and Observation | Preserves intellectual integrity through migration |
| _Templates and _Bases use underscore prefix | Groups system files at bottom of explorer on all platforms |
| No Tasks plugin | Statuses are properties, not task lists |
| No DB Folder plugin | Superseded by native Bases |
| No Charts plugin | Dataview tables sufficient for Phase 1-2 analytics |

---

## 23. DECISIONS INTENTIONALLY DEFERRED

| Decision | Reason |
|---|---|
| CSS snippet / theme selection | Requires testing on desktop and mobile. Phase 2. |
| Exact Meta Bind widget syntax per template | Must be tested against Meta Bind 1.5.1. Phase 2. |
| DataviewJS queries for variable combination analysis | Requires real trade data to validate. Phase 3. |
| Account currency label | Not specified by user. Added when confirmed. |
| Exact variable names (Short Variable, Sub Variable, etc.) | User confirmation needed before creating Variable notes. |
| Trade ID sequence counter mechanism | Templater counter file vs. datetime suffix. Resolved in Phase 2. |
| Canvas usage for strategy visualization | Available; specific designs deferred until user confirms interest. |
| Archive threshold policy | User preference. Phase 4+. |
| Additional assets list | Created on demand. No pre-population without user input. |
| Payout percentages per asset | Varies by broker. Property available but not pre-populated. |
| Obsidian theme selection | Phase 2, after core structure is stable. |

---

## 24. PHASE 2 SCOPE

### Priority 1 â€” Foundation
1. Create complete folder structure (all folders documented in Section 6)
2. Create all 16 Templater templates in _Templates/
3. Configure QuickAdd with all 16 commands mapped to templates
4. Create reference notes: market regime notes in 04-Market/Regimes/, session type notes in 04-Market/Sessions/
5. Create placeholder variable notes in 05-Variables/ (pending user confirmation of exact names)

### Priority 2 â€” Dashboard Framework
6. Build Trading OS home dashboard with navigation, quick actions (Meta Bind), and live Dataview queries
7. Build remaining 5 dashboard stubs
8. Create Bases view files in _Bases/

### Priority 3 â€” Validation
9. Full New Trade workflow test on desktop
10. Full New Trade workflow test on mobile (iOS)
11. Verify Bases views render correctly
12. Verify Dataview win rate query
13. Verify Meta Bind dropdowns on mobile
14. Document any compatibility issues discovered

### Priority 4 â€” Styling
15. Apply CSS snippet for professional dark-mode visual design
16. Configure Obsidian appearance settings

### Not in Phase 2
- OneNote migration (Phase 3)
- DataviewJS variable combination queries (Phase 3, after real data exists)
- Archive system (Phase 4+)
- Advanced performance analytics (Phase 3+)

---

*End of ARCHITECTURE.md*
*Phase 1 Complete â€” Awaiting user approval before Phase 2 implementation*
*Last updated: 2026-08-24*
