# Quotex Binary Options Trading OS Migration Report

## 1. Executive Summary

This report outlines the findings of a technical and structural audit performed on the existing Obsidian-based Trading OS repository. The current repository (`legendjournal`) was originally designed to accommodate both Forex and Quotex Binary Options trading, but acts primarily as a dual-system (or Forex-first) environment where `trade-type` distinguishes between "FOREX" and "BINARY".

The objective of this migration is to pivot the entire architecture into a dedicated **Quotex Binary Options Trading OS**, abandoning any unnecessary Forex baggage. The migration will restructure templates, dashboards, and system metadata to natively support Quotex Binary Options concepts (e.g., Fixed Expiry, CALL/PUT, Payout, Stake, and OTC algorithmic behavior) as the foundational model rather than an alternative `trade-type`.

The audit evaluated all components, identified what is inherently Forex-specific vs. Generic, highlighted areas of improvement, and proposed a migration plan to ensure minimal disruption to the existing robust review and knowledge-management structures.

## 2. Repository Structure

The `legendjournal` Obsidian vault is organized using a numbered prefix folder hierarchy, maximizing mobile navigability and chronological ordering.

- `00-OS/`: Core dashboards (e.g., Trading, Quotex Binary Options, Market, Strategy, Review) and system configuration.
- `01-Journal/`: Live trading records.
  - `Sessions/`: Daily session notes.
  - `Trades/`: Individual trade logs grouped by year/month.
  - `Reviews/`: Daily and weekly reviews.
- `02-Strategies/`: Strategy knowledge base, holding master records and specific versions.
- `03-Research/`: Research repository for experiments, backtests, and observations.
- `04-Market/`: Metadata notes for tradable instruments (`Assets`), market regimes (`Regimes`), behaviors (`Behaviors`), and session types (`Sessions`).
- `05-Variables/`: Technical and conceptual variables (e.g., SNR, Acceleration) used for confluences in trades.
- `06-Psychology/`: Notes on trading mistakes and general psychological observations.
- `07-Knowledge/`: Atomic notes, rules, and concepts.
- `08-Evidence/`: Screenshots and supporting materials.
- `_Templates/`: Templater definitions for generating the above structured notes.
- `_Bases/`: Configuration files for the Obsidian Bases plugin (database views).

This structure enforces a "Properties over Folders" approach, heavily leveraging YAML frontmatter to cross-reference data.

## 3. Current Architecture

The current architecture is highly structured and automation-driven.

- **Data Model:** Almost all critical data is stored in YAML frontmatter. Obsidian wiki-links (e.g., `[[AST-EUR-USD]]`) act as foreign keys, linking Trades to Assets, Strategies, Sessions, and Variables.
- **Template Generation:** The `Templater` and `QuickAdd` community plugins handle note creation. Templates use `tp.system.suggester` to prompt users for inputs (like Trade Type, Asset, Direction, Result) during creation and automatically route files to correct subfolders.
- **Dashboards:** Built with `Dataview` and `Meta Bind`. Dataview dynamically aggregates trade data, win rates, and P/L. Meta Bind provides buttons for executing QuickAdd macros (e.g., "+ NEW TRADE").
- **Controlled Vocabularies:** Fields like `direction`, `result`, `market-regime`, and `asset-class` use strict enum-like sets enforced by configuration and templates.
- **Dual Support (Forex/Binary):** Currently, the system prompts for `trade-type` ("FOREX" or "BINARY") in the trade template. `Dashboard - Trading.md` acts as a generic (but heavily Forex-leaning) dashboard, while `Dashboard - Quotex Binary Options.md` attempts to filter specifically for BO trades (`WHERE trade-type = "BINARY"`).

## 4. Component-by-Component Analysis

*   **Dashboards (`00-OS/`)**:
    *   `Dashboard - Trading OS.md`: The main entry point. Currently shows aggregate statistics across *all* trade types.
    *   `Dashboard - Trading.md`: The default trading view. Shows generic or Forex-oriented data.
    *   `Dashboard - Quotex Binary Options.md`: A separate view explicitly filtering for `trade-type = "BINARY"`. Evaluates Payout, Stake, and OTC Market Behaviors.
*   **Trade Template (`_Templates/TPL-Trade.md`)**:
    *   Prompts user for "Trade Type" (FOREX or BINARY).
    *   Checks if an asset is "OTC" (Binary specific) and prompts for OTC-specific `market-behavior`.
    *   Asks for "Direction" (CALL/PUT) and hardcodes `expiry` to "5m", `payout` to 85, and `stake` to 10.
*   **Session & Review Templates**:
    *   Provide high-level win-rate calculations but assume a unified trading strategy.
*   **Market Notes (`04-Market/`)**:
    *   Assets (`AST-*.md`) explicitly define `asset-class: Forex` and `asset-type: Live` or `OTC`.
    *   Regimes (`REG-*.md`) represent Forex structural states (Normal, Reversal, Choppy, Trending).
*   **Variables (`05-Variables/`)**:
    *   Represents confluences (SNR, Short, Sub, Events). They are fundamentally generic technical analysis components, highly compatible with BO.
*   **Data Dictionary & Architecture Docs**:
    *   Maintain strict definitions that bridge both worlds, leading to bloated schemas (e.g., storing `trade-type`, `pips` [implied in Forex], alongside `payout` and `stake`).

## 5. Forex-Specific Components

The following components are designed around Forex mechanics and concepts.

*   **`trade-type` Property**: The existence of a toggle between FOREX and BINARY implies a Forex-first architecture. In a pure BO system, this field is redundant.
*   **Asset Classification (`asset-class: Forex`)**: In templates (`TPL-Asset.md`), "Forex" is the default asset class. While BO trades Forex pairs (e.g., EUR/USD), the *asset class* in BO context is often differentiated more by OTC vs Live rather than Forex vs Commodity.
*   **Session Types (e.g., "London", "New York")**: Forex trading heavily revolves around specific global market opens. Quotex Binary Options (especially OTC on platforms like Quotex) is often traded 24/7 or relies on different session logic. `SES-TYPE-London.md` is a Forex paradigm.
*   **Market Regimes ("Trending", "Choppy")**: While applicable to BO, the specific terminology used in the system currently reflects classic Forex macro-trend analysis, whereas BO focuses heavily on micro-structure (e.g., 1-minute candle behavior).
*   **Dashboard - Trading.md (Generic View)**: This dashboard acts as the de-facto Forex dashboard by omitting BO specific calculations (like Stake and Payout) in its primary views.
*   **"Net P/L" logic without Payout**: Forex relies on dynamic risk/reward (pips/lots/leverage). BO relies on fixed payout (`stake * (payout/100)`). The system struggles to unify these in the generic dashboard.

**Why classified this way?** These components rely on continuous price movement, dynamic exits, and global macro sessions, rather than fixed-time, fixed-yield mechanics.

## 6. Generic Components

These components are market-agnostic and form the backbone of the "Trading OS" concept. They should be retained entirely.

*   **Psychology Tracking (`06-Psychology/`)**: Bias types (FOMO, Revenge, Tilt), mental state tracking, and mistake categorization are universal to all trading.
*   **Review System (`TPL-DailyReview.md`, `TPL-WeeklyReview.md`)**: The process of reflecting on a trading day/week, tracking win-rates, and grading psychology is universal.
*   **Research & Evidence (`03-Research/`, `08-Evidence/`)**: The core hypothesis-testing framework (Experiments, Observations, Backtests) and screenshot management are excellent. However, `03-Research` will need to be significantly expanded to accommodate deep candlestick and sequence research for the Quotex OTC markets.
*   **Variables (`05-Variables/`)**: Confluence factors like Support/Resistance (SNR) are the foundation of technical analysis in both BO and Forex.
*   **Strategy Versioning (`02-Strategies/`)**: Tracking strategy changelogs and versions is critical software-engineering style discipline applicable anywhere.
*   **Core Architecture Mechanics**: The use of QuickAdd, Templater, Dataview, and Meta Bind for structured data entry and retrieval is highly effective.

## 7. Quotex Binary Options Requirements

To function as a dedicated Quotex Binary Options OS, the system must natively support and prioritize these concepts:

*   **Fixed Expiry:** The exact duration of the trade (e.g., 1m, 2m, 5m). *Currently exists in the schema (`expiry`), but needs to be promoted to a primary filter/dashboard metric.*
*   **Direction (CALL / PUT):** Binary options are strictly directional bets. *Currently exists and is prompted in `TPL-Trade.md`.*
*   **Stake, Payout & Expiry Data Capture:** Quotex returns are a fixed percentage (`payout`) of the risked amount (`stake`). *Currently exists but is hardcoded in `TPL-Trade.md` (Stake: 10, Payout: 85, Expiry: 5m) instead of being dynamically captured.* These values must NOT be hardcoded going forward. They need to be entered per trade or captured from the actual Quotex trade context.
*   **OTC Analysis Deep Dive:** Quotex OTC markets are algorithmically generated and require deep, specific tracking. The current `market-behavior: Normal/Reversal` is insufficient. The architecture must be expanded to meticulously record OTC-specific data:
    *   **Candle Behavior:** Tracking specific formation speeds, algorithmic ticks, and anomalies.
    *   **Sequence:** The exact sequence of candles leading to a setup.
    *   **Setup & Context:** The broader algorithmic structure (is the algorithm trapping traders? creating fake breakouts?).
    *   **Outcome:** Highly detailed outcome tracking beyond simple WIN/LOSS (e.g., 1-pip loss due to algorithmic manipulation, deep win vs close win).
*   **Micro-Structure Focus:** BO strategies often rely on specific candle formations or second-by-second confluences rather than macro sessions. *The `Variables` system maps well to this.*
*   **High-Frequency Capability:** BO traders often take more trades per session than Forex traders. The system must support rapid entry. *The QuickAdd macro system is already capable of this.*

## 8. Problems / Risks / Inconsistencies

During the audit, several architectural friction points were identified:

1.  **Hardcoded Values in Trade Template:** `TPL-Trade.md` hardcodes `expiry: "5m"`, `payout: 85`, and `stake: 10`. This creates inaccurate data if the user doesn't manually edit the YAML every time. These fields must be prompted per trade or captured from context.
2.  **Dashboard Fragmentation:** Having a `Dashboard - Trading.md` and a `Dashboard - Quotex Binary Options.md` creates confusion. If the vault is exclusively for BO, the "Generic" trading dashboard is redundant and confusing.
3.  **Net P/L Calculation Complexity:** The Dataview queries use complex inline logic to calculate Quotex profits: `choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0))`. This is repeated across multiple dashboards. To prevent inconsistencies caused by manual editing, `net-pl` should be calculated dynamically from the underlying fields (`stake`, `payout`, `result`), either via DataviewJS across the OS, or via a central view, rather than maintaining a manually editable property in the YAML frontmatter.
4.  **Forex Remnants in Templates:** The `TPL-Trade.md` prompts for `tradeType` (FOREX/BINARY). This extra step slows down data entry in a pure BO system.
5.  **Market Regime vs Behavior:** The system uses `market-regime` (Forex style) but also added `market-behavior` (OTC style). These overlap conceptually and need to be unified or clearly delineated for BO.
6.  **`net-pl: 0` Default:** The trade template defaults `net-pl` to 0, but Dataview recalculates it dynamically. This means the static property is ignored, creating a data inconsistency.

## 9. Migration Boundary: KEEP / MODIFY / REMOVE

### A. KEEP (Unchanged or minor cosmetic tweaks)
*   **Folder Structure:** The `01` through `08` prefix system is excellent.
*   **Psychology, Review, and Knowledge Systems:** Templates and logic for these are domain-agnostic and well-designed.
*   **Variables System:** The `05-Variables/` structure is perfect for building confluences.
*   **Plugin Stack:** Dataview, Templater, QuickAdd, and Meta Bind are the correct tools for the job.

### B. MODIFY (Requires structural updates)
*   **`TPL-Trade.md`:** Remove the FOREX/BINARY prompt. Add dynamic prompts for Payout, Stake, and Expiry via `tp.system.prompt` to eliminate hardcoded values.
*   **Dashboards (`Dashboard - Trading OS.md`, `Dashboard - Trading.md`):** Merge the BO specific logic (Payout/Stake analytics, Expiry win-rates) into the primary Trading dashboards.
*   **Data Dictionary & Architecture Docs:** Update definitions to reflect the pure BO model. Remove references to Forex classes and concepts.
*   **Asset Templates/Notes:** Redefine `asset-class` to reflect BO reality (e.g., Currency Pair, Crypto) and elevate `asset-type` (Live vs OTC).

### C. REMOVE / REPLACE (To be deleted or entirely replaced)
*   **`Dashboard - Quotex Binary Options.md`:** This becomes redundant once the core system is fully BO-native.
*   **Forex Session Concepts (`SES-TYPE-London`, etc.):** Replace with BO-relevant timeframes or simply rely on time-of-day analytics.
*   **The `trade-type` Property:** Remove completely from all schemas and existing notes.

## 10. Proposed Target Architecture

The target architecture will be a **pure Quotex Binary Options OS**.

**Core Paradigm Shift:**
The system will no longer view Quotex Binary Options as a "mode" but as the fundamental reality of the database.

**Key Changes:**
1.  **Unified Trading Dashboard:** `Dashboard - Trading.md` will become the central hub, incorporating the Expiry, Direction, and OTC Behavior tables currently isolated in the BO dashboard. `Dashboard - Quotex Binary Options.md` will be deprecated.
2.  **Streamlined Trade Entry:** `TPL-Trade.md` will assume BO. It will immediately prompt for Asset, Direction, Expiry, Stake, and Payout. The `net-pl` will be calculated within the Templater script at creation time (based on stake/payout/result if known) or left for Dataview to aggregate.
3.  **OTC as a First-Class Citizen:** `asset-type: OTC` will trigger specific tracking workflows (like `market-behavior: Normal/Reversal`) natively, without relying on the now-removed `trade-type` check.
4.  **Simplified Metadata:** The `DATA DICTIONARY.md` will be purged of Forex terminology (pips, lots, leverage, FOREX trade-type).

## 11. Recommended Migration Plan

To ensure a safe transition without data loss, the migration should follow this strict sequence:

**Phase 1: Metadata & Documentation Core (Safe)**
*   Update `ARCHITECTURE.md` and `DATA DICTIONARY.md` to define the pure BO schemas.
*   Update `System - Config.md` to remove `FOREX` and `BINARY` from the controlled vocabularies.

**Phase 2: Template Refactoring (Low Risk)**
*   Modify `_Templates/TPL-Trade.md`: Remove `tradeType` prompt. Add prompts for Expiry, Stake, and Payout. Ensure `market-behavior` prompt triggers based on `asset-type` correctly.
*   Review all other templates (Session, Review, Asset) to ensure no hardcoded Forex assumptions remain.

**Phase 3: Dashboard Consolidation (Medium Risk)**
*   Migrate all valuable Dataview queries from `Dashboard - Quotex Binary Options.md` into `Dashboard - Trading.md`.
*   Update `Dashboard - Trading OS.md` to reflect the new primary views.
*   Update navigation headers (`<div class="tos-nav">`) across all dashboards to remove the "BINARY" link.
*   Delete `Dashboard - Quotex Binary Options.md`.

**Phase 4: Historical Data Preservation (High Risk)**
*   **Do not blindly delete `trade-type`**. Historical data is valuable. We will preserve the `trade-type` property in existing notes to maintain the context of past trades, even as we move towards a Quotex-exclusive system going forward.
*   Ensure existing Quotex trades have correct `stake` and `payout` values populated. We will need to investigate the best way to handle historical trades that might lack this data.

**Phase 5: Validation & Testing**
*   Perform dummy trade entries via QuickAdd to ensure the new streamlined BO workflow functions smoothly on desktop and mobile.
*   Verify all Dataview queries render without errors.

## 12. Files Likely to Require Changes

*   `ARCHITECTURE.md`
*   `DATA DICTIONARY.md`
*   `00-OS/System - Config.md`
*   `_Templates/TPL-Trade.md`
*   `_Templates/TPL-Asset.md`
*   `00-OS/Dashboard - Trading OS.md`
*   `00-OS/Dashboard - Trading.md`
*   `00-OS/Dashboard - Market.md` (remove BO link in header)
*   `00-OS/Dashboard - Knowledge.md` (remove BO link in header)
*   `00-OS/Dashboard - Psychology.md` (remove BO link in header)
*   `00-OS/Dashboard - Research.md` (remove BO link in header)
*   `00-OS/Dashboard - Review.md` (remove BO link in header)
*   `00-OS/Dashboard - Strategy.md` (remove BO link in header)
*   `00-OS/Dashboard - Quotex Binary Options.md` (To be DELETED)
*   Existing Trade Notes in `01-Journal/Trades/` (Historical `trade-type` will be preserved, but stake/payout will be addressed).

## 13. Files That Should NOT Be Changed

*   `05-Variables/*` (The confluence variables are generic and highly useful).
*   `06-Psychology/*` (Mistakes and psychology tracking remain identical).
*   `03-Research/*` (While structural methodologies are sound, this folder will likely require significant extension to support the new, deeper OTC candlestick and sequence research requirements).
*   `02-Strategies/*` (Strategy versioning logic is sound).
*   `_Templates/TPL-DailyReview.md`
*   `_Templates/TPL-WeeklyReview.md`
*   `_Templates/TPL-Mistake.md`
*   `_Templates/TPL-Psychology.md`
*   `_Templates/TPL-Research.md`
*   `_Templates/TPL-Backtest.md`
*   `_Templates/TPL-Observation.md`

## 14. Unknowns / Questions Requiring Human Decisions

1.  **Historical Data Preservation:** Historical `trade-type` data will be preserved. How do we accurately backfill historical `stake` and `payout` values for existing Quotex trades without manual entry, or is manual backfilling the only option?
2.  **`net-pl` Calculation Standardization:** Given the decision to calculate `net-pl` dynamically from underlying fields to avoid manual errors, how should we best centralize this calculation to avoid repeating complex `choice` logic across multiple Dataview queries?
3.  **Market Regimes:** Do you want to keep the Forex-style regimes (Normal, Reversal, Choppy, Trending) for Live BO trading, or replace them entirely with OTC-style algorithmic behaviors across all assets?
4.  **Session Types:** Do Forex sessions (London, NY, Asian) hold relevance for your BO strategy, or should we replace them with time-blocks (e.g., "Morning", "Afternoon", "Night")?

## 15. Final Recommendations

The `legendjournal` repository is an exceptionally well-engineered personal operating system. The migration to a pure Quotex Binary Options architecture is entirely feasible and highly recommended to reduce cognitive load and data-entry friction.

By eliminating the dual-system overhead (`trade-type` checks, redundant dashboards) and elevating BO primitives (Stake, Payout, Expiry, OTC Behavior) to primary citizens, the OS will become significantly faster to use, especially on mobile devices.

Proceeding with the outlined Migration Plan (Phase 1-5) will safely transition the vault without compromising the powerful review, psychology, and research loops already in place.
