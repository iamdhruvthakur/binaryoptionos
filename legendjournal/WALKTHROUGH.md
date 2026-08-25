# WALKTHROUGH

> Complete guide to using the Trading OS at its full potential.

---

## System Philosophy

This vault is a **Binary Options Trading Research & Knowledge Operating System**. It is not a simple note-taking app.

Every note you create becomes a data point in an interconnected analytical system. Trades link to sessions. Sessions link to reviews. Mistakes link to psychology. Research links to evidence. Everything is queryable, filterable, and cross-referenced through Dataview and Bases.

**Core principles:**
- Every trade is documented with full context
- Every session is reviewed
- Every mistake is tracked and analysed
- Every hypothesis is tested through structured research
- Strategy evolution is versioned and auditable
- Knowledge progresses from idea to verified rule

---

## Vault Structure

| Folder | Purpose |
|---|---|
| `00-OS/` | Dashboards, system config, navigation hub |
| `01-Journal/` | Trades, Sessions, Daily/Weekly Reviews |
| `02-Strategies/` | Strategy registry, versions, changelogs |
| `03-Research/` | Experiments, backtests, observations |
| `04-Market/` | Assets, market regimes, session types |
| `05-Variables/` | Trading variables (SNR, Short, Sub, etc.) |
| `06-Psychology/` | Mistakes, psychology observations |
| `07-Knowledge/` | Rules, concepts, imported knowledge |
| `08-Evidence/` | Screenshots, charts, attachments |
| `_Templates/` | Templater templates (do not edit directly) |
| `_Bases/` | Obsidian Bases database views |

---

## Getting Started

1. Open the vault in Obsidian
2. Navigate to **Dashboard - Trading OS** (the Home dashboard)
3. Verify that the CSS snippet `trading-os` is enabled in Settings > Appearance > CSS Snippets
4. The system is ready when you see the Home dashboard with Quick Action buttons

---

## Daily Trading Workflow

### Before Trading

1. Open the **Home Dashboard** (`Dashboard - Trading OS`)
2. Check the **System Status** -- your active strategy and version
3. Create a new **Session** using the `+ SESSION` button
4. Select the session type (London, New York, etc.)
5. Select the market regime (Normal, Reversal, Choppy, Trending)
6. Note your mental state in the Pre-Session section

### Taking Trades

1. Use the `+ NEW TRADE` button for each trade
2. Select the asset from the suggester (e.g. EUR-USD)
3. Select direction (CALL or PUT)
4. Optionally select the result immediately, or leave empty and fill later
5. The trade note opens automatically -- fill in:
   - **Trade Context** -- what you saw before entering
   - **Setup Description** -- check the variable checklist
   - **Entry Analysis** -- why you entered
   - **Trade Outcome** -- result, payout, stake
   - **Post-Trade Analysis** -- what happened and why

### After Trading

1. Complete the Session note with a summary
2. Create a **Daily Review** using `+ DAILY REVIEW`
3. Fill in performance metrics (total trades, wins, losses)
4. Rate your psychology (1-5 scale)
5. Record what went well and what to improve
6. Flag any mistakes on individual trade notes

### Linking Trades to Sessions

In each trade note, set the `session-ref` property to link to the session:
```
session-ref: "[[SES-20260824-1400-XXXX]]"
```

In the session note, add each trade to the `trades` list:
```
trades: ["[[TRD-20260824-140500-XXXX]]", "[[TRD-20260824-142000-XXXX]]"]
```

---

## Weekly Review Workflow

1. At the end of each trading week, use QuickAdd command **04 Weekly Review**
2. The template auto-generates the week number and year
3. Link all daily reviews from the week in the `daily-reviews` property
4. Fill in:
   - Performance by regime (table provided in template)
   - Performance by asset
   - Key discoveries
   - Strategy notes
   - Recurring mistakes
   - Goals for next week

---

## Strategy Evolution

When you discover something that changes your trading rules:

1. **Create a Changelog** (`+ CHANGELOG` on Strategy dashboard)
   - Document what changed and why
   - Reference supporting evidence or research
2. **Create a new Strategy Version** (`+ NEW VERSION`)
   - Document the full updated rule set
   - Link to the changelog
3. **Update the Strategy master note** (`[[STR-V6]]`)
   - Update `current-version` to the new version
   - Add the new version to the versions list
4. **Update System Config** (`[[System - Config]]`)
   - Update `current-version` to the new version

### Adding a New Strategy

If you develop an entirely new strategy (not a version of V6):

1. Use QuickAdd command **05 New Strategy**
2. Give it a short name (e.g. V7)
3. This creates `STR-V7` in `02-Strategies/Registry/`
4. Then create versions under it

> **Note:** The current templates hardcode `[[STR-V6]]` as the default strategy. If you add a new strategy, you may want to update the template defaults.

---

## Research Workflow

### Starting an Experiment

1. Use `+ NEW EXPERIMENT` on the Research dashboard
2. Write a clear research question
3. State your hypothesis explicitly (this is critical)
4. Define your method, sample size, and data period
5. Link relevant variables and conditions

### Running the Experiment

1. Update the status to `In Progress`
2. Record observations as you gather data
3. Add evidence (screenshots, charts) as you go
4. Track your sample size

### Completing the Experiment

1. Write your conclusion
2. Set `conclusion-type`:
   - **CONFIRMED** -- the hypothesis was validated
   - **REFUTED** -- the hypothesis was disproven
   - **INCONCLUSIVE** -- insufficient evidence
   - **PARTIAL** -- partially supported
3. Update status to `Completed`
4. If CONFIRMED, create a RULE in Knowledge (`+ NEW KNOWLEDGE`, select "RULE")

---

## Mistake Tracking

### Flagging a Mistake

1. On the trade note, set `mistake: "[[MST-Early-Entry]]"` (or the appropriate mistake)
2. Set `psychology-flag: true` if psychology was a factor
3. If the mistake type does not exist yet, create it via `+ NEW MISTAKE`

### Reviewing Mistakes

1. Open the **Psychology Dashboard**
2. The **Mistake Registry** shows all defined mistakes with frequency and status
3. The **Mistake Frequency (from Trades)** shows how often each mistake appears and its association with losses
4. Use this data to identify your most costly behavioral patterns

---

## Evidence Management

1. Take a screenshot of the relevant chart or data
2. Use `+ EVIDENCE` on the Research dashboard
3. Select the evidence type (Screenshot, Chart, Annotation, etc.)
4. Paste or embed the image in the note body
5. Link it to the relevant trade, research, or observation using the frontmatter properties

---

## Dashboard Usage

### Home (Trading OS)
Your command center. Quick Actions, performance snapshot, today's activity, items needing attention.

### Trading
Deep performance analysis for Binary Options. Win rates by regime, asset, session, and day of week. Mistake impact analysis. Full trade log.

### Binary Options
Dedicated performance tracking for OTC algorithmic markets. Analyzes Stake efficiency, Payout structures, Net P/L, and `NORMAL` vs `REVERSAL` market behavior win-rates without polluting Forex data.

### Strategy
Strategy version registry, live performance by version, changelogs, variables, backtests.

### Research
Research pipeline status, active experiments, completed research, confirmed/rejected findings, backtests, observations.

### Market
Market regime reference and performance data. Session type reference with UTC/IST times. Registered assets. Market observations.

### Psychology
Mistake registry and frequency analysis. Psychology-flagged trades. Bias patterns. Psychology rating trend from daily reviews.

### Review
Review completion status. Unreviewed sessions and trades. Recent daily and weekly reviews. 30-day consistency view.

### Knowledge
Rules, concepts, information type distribution. Imported knowledge tracking. Recent knowledge notes.

---

## Mobile Workflow

The system is designed to work on iPhone, iPad, and Android devices via Obsidian Mobile.

### Quick Trade Entry (Mobile)

1. Open Obsidian Mobile
2. Navigate to Home dashboard (set it as your startup file)
3. Tap `+ NEW TRADE`
4. Select asset, direction, and result from the suggesters
5. The trade note is created and opened -- fill in context later

### Tips for Mobile

- Use the Quick Switcher (swipe down) to jump between dashboards
- The navigation bar at the top of each dashboard works as links
- Tables scroll horizontally on small screens
- Buttons are sized for touch (44px minimum)
- Properties can be edited via Obsidian's property editor

---

## System Maintenance

### Regular Tasks

| Task | Frequency | How |
|---|---|---|
| Create Daily Review | Daily | `+ DAILY REVIEW` |
| Create Weekly Review | Weekly | QuickAdd 04 |
| Review unreviewed sessions | As needed | Review Dashboard |
| Update strategy version | When rules change | Strategy Dashboard |
| Back up vault | Weekly | Obsidian Sync or manual copy |

### Troubleshooting

**QuickAdd buttons not working:**
1. Open Settings > Community Plugins > QuickAdd > Options
2. Verify that all 16 choices are listed
3. Ensure each choice has `Command` enabled
4. Restart Obsidian if needed

**Dataview queries showing nothing:**
- This is normal when no data exists yet
- Empty states are shown below each query
- Create your first session and trades to see data

**CSS not applying:**
1. Open Settings > Appearance > CSS Snippets
2. Toggle on `trading-os`
3. If the file does not appear, check that `.obsidian/snippets/trading-os.css` exists

**Meta Bind buttons not rendering:**
- Ensure the Meta Bind plugin is enabled
- Check that the code block language is exactly `meta-bind-button`
- Restart Obsidian after enabling the plugin

---

## QuickAdd Command Reference

| # | Command | Creates | Destination |
|---|---|---|---|
| 01 | New Trade | Trade note | `01-Journal/Trades/YYYY/` |
| 02 | New Session | Session note | `01-Journal/Sessions/YYYY/` |
| 03 | Daily Review | Daily review | `01-Journal/Reviews/YYYY/` |
| 04 | Weekly Review | Weekly review | `01-Journal/Reviews/YYYY/` |
| 05 | New Strategy | Strategy master | `02-Strategies/Registry/` |
| 06 | New Strategy Version | Version note | `02-Strategies/Versions/` |
| 07 | New Changelog | Changelog note | `02-Strategies/Changelogs/` |
| 08 | New Research | Experiment note | `03-Research/Experiments/` |
| 09 | New Backtest | Backtest note | `03-Research/Backtests/` |
| 10 | New Observation | Observation note | `03-Research/Observations/` |
| 11 | New Mistake | Mistake note | `06-Psychology/Mistakes/` |
| 12 | New Psychology | Psychology note | `06-Psychology/Observations/` |
| 13 | New Evidence | Evidence note | `08-Evidence/` |
| 14 | New Asset | Asset note | `04-Market/Assets/` |
| 15 | New Variable | Variable note | `05-Variables/` |
| 16 | New Knowledge | Knowledge note | `07-Knowledge/Rules/` or `Concepts/` |

---

## Note ID Format

All notes use readable, sortable IDs:

| Type | Format | Example |
|---|---|---|
| Trade | `TRD-YYYYMMDD-HHmmss-XXXX` | TRD-20260824-143022-A7F2 |
| Session | `SES-YYYYMMDD-HHmm-XXXX` | SES-20260824-1400-B3K9 |
| Daily Review | `REV-D-YYYY-MM-DD` | REV-D-2026-08-24 |
| Weekly Review | `REV-W-YYYY-WNN` | REV-W-2026-W34 |
| Research | `EXP-YYYYMMDD-HHmmss-XXXX` | EXP-20260824-150000-C2D4 |
| Backtest | `BT-YYYYMMDD-HHmmss-XXXX` | BT-20260824-160000-E5F1 |
| Observation | `OBS-YYYYMMDD-HHmmss-XXXX` | OBS-20260824-170000-G8H3 |
| Evidence | `EVD-YYYYMMDD-HHmmss-XXXX` | EVD-20260824-180000-I4J6 |
| Psychology | `PSY-YYYYMMDD-HHmmss-XXXX` | PSY-20260824-153500-K1L2 |
| Strategy | `STR-Name` | STR-V6 |
| Version | `VER-VN.N` | VER-V6.2 |
| Changelog | `CL-VN.N` | CL-V6.2 |
| Mistake | `MST-Name` | MST-Early-Entry |
| Asset | `AST-Name` | AST-EUR-USD |
| Variable | `VAR-Alias` | VAR-SNR |
| Knowledge | `KNW-Title` | KNW-Price-Action-Rule |

The `XXXX` suffix is a random 4-character base36 identifier that prevents collisions when creating multiple notes within the same second.

---

## Knowledge Promotion Path

Knowledge notes progress through a hierarchy:

```
UNVERIFIED-IDEA  -->  Test it
PERSONAL-OPINION -->  Research it
OBSERVATION      -->  Create experiment
HYPOTHESIS       -->  Run experiment
EXPERIMENT       -->  Complete it
CONCLUSION       -->  Verify it
FACT             -->  Stable reference
RULE             -->  Confirmed trading rule
```

To promote a note, change its `information-type` property and move it to the appropriate folder if needed (e.g. from `Concepts/` to `Rules/`).

---
*[[Dashboard - Trading OS|Home]] | [[SYSTEM GUIDE|System Guide]] | [[WORKFLOW GUIDE|Workflow Guide]] | [[DATA DICTIONARY|Data Dictionary]]*