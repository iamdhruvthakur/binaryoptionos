# Quotex Dashboard Architecture Proposal

This document outlines the target dashboard architecture for the Quotex Binary Options Trading OS, based on the findings of the Phase 1 Forensic Audit.

**Objective:** Transform the dashboards from a fragmented, dual-system statistical view into a unified, mobile-first Functional Trading Interface that deeply integrates the `Research -> Strategy -> Trade -> Review` feedback loop.

## 1. Dashboard Component Hierarchy

The system relies on 6 primary dashboards. `Dashboard - Binary Options.md`, `Dashboard - Psychology.md`, and `Dashboard - Knowledge.md` are deprecated or merged to reduce cognitive load and fragmentation.

`
00-OS/
├── Dashboard - Trading OS.md    (Home / Control Center)
├── Dashboard - Trading.md       (Primary Analytics & Log)
├── Dashboard - Strategy.md      (Registry & Versioning)
├── Dashboard - Research.md      (Deep OTC/Candle Loop)
├── Dashboard - Market.md        (Asset & Behavior DB)
└── Dashboard - Review.md        (Psychology & Workflow)
`

### Global Navigation Header
All dashboards will share a unified `<div class="tos-nav">` header:
`HOME | TRADING | STRATEGY | RESEARCH | MARKET | REVIEW`

## 2. Dashboard Layouts & Data Dependencies

### A. HOME / TRADING OS (`Dashboard - Trading OS.md`)
**Purpose:** The main control center and launchpad.
*   **System Status:** Static links to Current Strategy, Version, and overall Status.
*   **Quick Actions (Meta Bind):** Buttons for `New Trade`, `New Session`, `Daily Review`, `Research`, and `Observation`.
*   **Today's Activity:**
    *   Dataview table showing today's trades (Time, Asset, Direction, Expiry, Result, P/L).
*   **Core Performance (Glance):**
    *   DataviewJS aggregate of All-Time, 30D, and 7D (Trades, Win Rate, Net P/L).
*   **Action Required (Alerts):**
    *   Unreviewed Sessions (Dataview: `WHERE note-type = "session" AND reviewed = false`)
    *   Unreviewed Trades (Dataview: `WHERE note-type = "trade" AND reviewed = false`)
*   **Recent Mistakes:**
    *   Trades in the last 7 days where `mistake != ""` or `psychology-flag = true`.

### B. TRADING DASHBOARD (`Dashboard - Trading.md`)
**Purpose:** Primary trading analytics, replacing the fragmented FOREX/BINARY views.
*   **Core Performance:** DataviewJS table calculating Total Trades, Wins, Losses, Voids, Win Rate, Avg Stake, Avg Payout, and dynamically calculated Net P/L.
*   **Time Analysis:**
    *   Day of Week performance (Dataview: `GROUP BY day-of-week`).
    *   *Note: Forex geographic sessions are removed. Time-of-day analytics will rely on standard hour extraction if technically practical in DataviewJS.*
*   **Quotex Trade Analysis (Grouped Tables):**
    *   Performance by **Asset** (Live vs OTC distinction derived from Asset note).
    *   Performance by **Direction** (CALL vs PUT).
    *   Performance by **Expiry** (1m, 2m, 5m, etc.).
    *   Performance by **Market Behavior** (NORMAL, REVERSAL, UNKNOWN).
    *   Performance by **Variables/Confluences** (Requires DataviewJS to parse array intersection).
    *   Performance by **Strategy Version**.
*   **Trade Quality & Feedback Loop:**
    *   Table highlighting trades with attached `evidence`, `mistake`, or specific `candle-behavior`/`pattern` notes to feed back into Research.
*   **Master Log:** Link to `_Bases/Trades.base` for deep tabular filtering.

### C. RESEARCH DASHBOARD (`Dashboard - Research.md`)
**Purpose:** The engine of the OS. Tracks the deep OTC structural loop.
*   **Active Pipeline:** Meta Bind buttons for `New Experiment`, `New Backtest`, `Observation`.
*   **OTC / Deep Structure Loop:**
    *   Dataview table of trades grouped by `candle-behavior`.
    *   Dataview table of trades grouped by `sequence`.
    *   Dataview table of trades grouped by `pattern`.
    *   *This directly fulfills the `Market → Candles → Sequence → Pattern` requirement.*
*   **Experiments:** Table of `research-experiment` notes `WHERE status = "Open" OR status = "In Progress"`.
*   **Discoveries/Conclusions:** Table of `knowledge` or `research-experiment` notes `WHERE conclusion-type = "CONFIRMED"`.

### D. STRATEGY DASHBOARD (`Dashboard - Strategy.md`)
**Purpose:** Version control and strategy efficacy.
*   **Active Strategies:** Dataview table of `strategy` notes.
*   **Version Performance:** Dataview table joining `strategy-version` with Trade data to show Trades, Win Rate, and Net P/L per version.
*   **Recent Changes:** Table of `strategy-changelog` notes.
*   **Supporting Research:** List of `research-experiment` notes linked to active strategies.

### E. REVIEW DASHBOARD (`Dashboard - Review.md`)
**Purpose:** Workflow completion, psychology, and continuous improvement.
*   **Workflow Queues:**
    *   Unreviewed Sessions (Needs Daily Review).
    *   Unlinked Daily Reviews (Needs Weekly Review).
*   **Psychology & Mistakes:**
    *   *Incorporates the old Psychology dashboard.*
    *   Recurring Mistakes table (Dataview: `GROUP BY mistake` on Trades).
    *   Recent `psychology-observation` notes.
*   **Historical Reviews:** Links to `_Bases/Reviews.base`.

### F. MARKET DASHBOARD (`Dashboard - Market.md`)
**Purpose:** Asset registry and algorithmic behavior tracking.
*   **Quotex Assets:** Table of `asset` notes categorized by `asset-type` (Live vs OTC).
*   **Regimes & Behaviors:**
    *   Table of `market-regime` notes (Legacy/Live).
    *   Table of `market-behavior` notes (OTC algorithms).
*   **Asset-Specific Observations:** Dataview linking `observation` notes to specific Assets.

## 3. Technical Data Dependencies & DRY Principles

To solve the "Net P/L Monster" (duplicated complex calculations identified in the audit) and ensure the dashboards scale:

1.  **DataviewJS Centralization:**
    *   We will introduce a single DataviewJS script (e.g., `_Scripts/calc.js` if permitted, or standardized inline JS) to handle the `Net P/L` calculation: `(result == "WIN" ? stake * (payout/100) : (result == "LOSS" ? -stake : 0))`.
    *   If external JS is not permitted, we will strictly utilize Dataview DQL but minimize repetition by keeping core performance metrics localized to `Dashboard - Trading.md` and the Home screen, avoiding scattering them across 10 different files.
2.  **Schema Source of Truth:**
    *   No properties will be invented. We will rely strictly on `result`, `stake`, `payout`, `expiry`, `direction`, `asset`, `market-behavior`, `candle-behavior`, `sequence`, and `pattern` as defined in `DATA DICTIONARY.md`.
3.  **Bases Integration:**
    *   Dashboards will provide high-level aggregations (GROUP BY).
    *   Granular, row-by-row filtering will be pushed to the `_Bases/*.base` files to preserve mobile performance and avoid overwhelming the markdown views.

## 4. Implementation Order (Phase 2)

This implementation is purely structural and completely reversible.

*   **Step 1:** Fix the global `<div class="tos-nav">` header across all remaining 6 core dashboards (removing deprecated links).
*   **Step 2:** Refactor `Dashboard - Trading OS.md` (Home) to the new streamlined layout.
*   **Step 3:** Refactor `Dashboard - Trading.md` (incorporating the Expiry/Payout/Behavior tables from the deleted Binary dashboard). Remove all `trade-type = "BINARY"` filters.
*   **Step 4:** Refactor `Dashboard - Research.md` to include the deep OTC loop tables (Candle, Sequence, Pattern).
*   **Step 5:** Refactor `Dashboard - Review.md` to incorporate Psychology/Mistakes tracking.
*   **Step 6:** Safely delete `Dashboard - Binary Options.md`, `Dashboard - Psychology.md`, and `Dashboard - Knowledge.md`.
