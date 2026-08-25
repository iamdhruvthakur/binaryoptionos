# Dashboard Forensic Audit Report

## 1. Dashboard Dependency Map

The Trading OS relies on 9 primary dashboards located in `00-OS/`. They are highly interconnected through a common HTML navigation header (`<div class="tos-nav">`) and utilize a mix of community plugins.

**Plugin Dependencies:**
*   **Dataview:** 63 total queries used across all dashboards for aggregations (win rate, trade counts, P/L).
*   **Meta Bind:** 27 total buttons used to trigger QuickAdd commands.
*   **QuickAdd:** Acts as the routing layer for note creation.
*   **Bases:** Used as the fallback for raw database views (e.g., `_Bases/Trades.base`).

**Dashboard Roles:**
*   `Dashboard - Trading OS.md` (Home, 9 queries, 6 buttons)
*   `Dashboard - Trading.md` (Core analytics, 10 queries, 2 buttons)
*   `Dashboard - Binary Options.md` (Targeted analytics, 11 queries, 5 buttons)
*   `Dashboard - Strategy.md` (Strategy versions, 5 queries, 3 buttons)
*   `Dashboard - Research.md` (Experiments/Backtests, 7 queries, 4 buttons)
*   `Dashboard - Psychology.md` (Mistakes, 6 queries, 2 buttons)
*   `Dashboard - Review.md` (Session/Daily reviews, 5 queries, 2 buttons)
*   `Dashboard - Market.md` (Assets/Regimes, 5 queries, 2 buttons)
*   `Dashboard - Knowledge.md` (Concepts/Rules, 5 queries, 1 button)

## 2. Broken/Mismatched Property List

*   **`net-pl`:** The templates define `net-pl` as a static property, but the dashboards completely ignore it.
*   **`trade-type`:** As of Phase 1, `trade-type` is now `[HISTORICAL]`. However, many active dashboard queries rely on `trade-type = "BINARY"`.
*   **`market-behavior` vs `market-regime`:** The system uses both. The dashboards group by both independently. With the shift to Quotex, `market-behavior` (OTC) needs to be the primary structural grouping for trades, alongside or replacing `market-regime`.

## 3. Obsolete Forex References

*   **`Dashboard - Trading.md` Filters:** The queries in the generic Trading dashboard still group by `trade-type` and state: *> No trade type data. Trades are classified as FOREX or BINARY.* This is an obsolete paradigm.
*   **`Dashboard - Binary Options.md` Existence:** The very existence of a separate "Binary Options" dashboard implies a dual-system (Forex + BO). In a native Quotex OS, the generic `Dashboard - Trading.md` *is* the Binary Options dashboard.

## 4. Duplicate Analytics & Calculations

*   **The Net P/L Monster:** The exact same complex inline calculation is duplicated **12 times** across `Dashboard - Binary Options.md`, `Dashboard - Trading.md`, `Dashboard - Strategy.md`, and `Dashboard - Trading OS.md`:
    `round(sum(map(rows, (r) => choice(r.result = "WIN", r.stake * (r.payout/100), choice(r.result = "LOSS", -r.stake, 0)))), 2) as "Net P/L"`
    This is highly fragile. If the calculation logic ever needs to change (e.g., to account for broker fees or dynamic payouts correctly), it has to be updated in 12 different places.
*   **Win Rate:** The win rate calculation `round(length(filter(rows, (r) => r.result = "WIN")) / max(length(filter(rows, (r) => r.result = "WIN" OR r.result = "LOSS")), 1) * 100, 1) + "%" as "Win Rate"` is repeated in almost every table.

## 5. Missing Analytics (Based on Quotex Requirements)

*   **Research Loop Missing:** The dashboards have no queries connecting trades to specific `candle-behavior`, `sequence`, or `pattern` (which were added in Phase 1).
*   **Empty States are Misleading:** Many tables say "> *No trades recorded yet*" or "> *No directional data available*" which is fine for a blank vault, but the explanatory text often references legacy Forex concepts (e.g., "Behavior is classified when creating a binary trade: NORMAL, REVERSAL").

## 6. Navigation Problems

*   **Broken Global Nav:** Every single dashboard contains the link `[[Dashboard - Binary Options|BINARY]]` in its `<div class="tos-nav">` header. Because `Dashboard - Binary Options.md` is slated for deprecation/merger, all 9 dashboards have broken top-level navigation.

## 7. QuickAdd / Meta Bind Problems

*   **Valid Commands:** The Meta Bind buttons correctly map to QuickAdd commands (e.g., `quickadd:choice:01-new-trade`).
*   **Legacy Context:** The button `id: btn-trade-otc` in `Dashboard - Binary Options.md` is meant specifically for Binary trades, while `btn-trade` in `Dashboard - Trading.md` is generic. This split is obsolete.

## 8. Recommended Dashboard Architecture

To finalize the transition to a Quotex-native OS and fix these structural flaws, the following architecture is recommended:

1.  **Deprecate `Dashboard - Binary Options.md`:** Delete this file entirely.
2.  **Elevate `Dashboard - Trading.md`:** Migrate the useful tables from the deleted dashboard (Payout Analysis, Expiry Performance, OTC Behavior) into `Dashboard - Trading.md`.
3.  **Fix Global Navigation:** Remove `[[Dashboard - Binary Options|BINARY]]` from the `<div class="tos-nav">` block in all 8 remaining dashboards.
4.  **Remove `trade-type` Filters:** Strip `WHERE trade-type = "BINARY"` from all Dataview queries. The queries should simply query `WHERE note-type = "trade"`.
5.  **Centralize DataviewJS / Net P/L (Future Scope):** The duplicated inline `Net P/L` calculation should eventually be moved to a centralized DataviewJS script (`view.js`) to adhere to DRY principles, though fixing the immediate structural filters is a higher priority.
6.  **Add Research Analytics:** Add queries to `Dashboard - Research.md` or `Dashboard - Trading.md` that group trades by the new Quotex properties: `candle-behavior`, `sequence`, and `pattern`.

## 9. Priority Ranking of Problems

1.  **CRITICAL:** Remove obsolete `trade-type = "BINARY"` filters across all dashboards (they will fail as new trades won't have this property).
2.  **HIGH:** Merge `Dashboard - Binary Options.md` analytics into `Dashboard - Trading.md` and delete the redundant dashboard.
3.  **HIGH:** Fix the broken global `<div class="tos-nav">` across all files.
4.  **MEDIUM:** Update empty-state text to reflect the new Quotex-native terminology.
5.  **LOW (Technical Debt):** Refactor the duplicated `Net P/L` and `Win Rate` Dataview calculations into reusable DataviewJS scripts.
