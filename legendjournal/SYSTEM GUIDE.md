# SYSTEM GUIDE

> Complete user guide for the Trading OS Obsidian vault.

---

## GETTING STARTED

### Vault Structure

| Folder           | Purpose                                    |
| ---------------- | ------------------------------------------ |
| `00-OS/`         | Dashboards, system config, navigation      |
| `01-Journal/`    | Trades, Sessions, Reviews (daily/weekly)   |
| `02-Strategies/` | Strategy registry, versions, changelogs    |
| `03-Research/`   | Experiments, backtests, observations       |
| `04-Market/`     | Assets, regimes, session types             |
| `05-Variables/`  | Trading variables (SNR, Short, Sub, etc.)  |
| `06-Psychology/` | Mistakes, psychology observations          |
| `07-Knowledge/`  | Rules, concepts, imported knowledge        |
| `08-Evidence/`   | Screenshots, charts, attachments           |
| `_Templates/`    | Templater templates (do not edit directly) |
| `_Bases/`        | Obsidian Bases database views              |

---

## DAILY WORKFLOW

### Before Trading

1. Open [[Dashboard - Trading OS|Home Dashboard]]
2. Check [[System - Config|System Config]] for active strategy/version
3. Create a new **Session** using the "+ NEW SESSION" button
4. Note your mental state in the Pre-Session section

### During Trading

1. For each trade, use the "+ NEW TRADE" button
2. Fill in the properties as prompted
3. Record variable checklist, context, and analysis
4. Link screenshots via Evidence notes if needed

### After Trading

1. Complete the Session note with summary and observations
2. Create a **Daily Review** using the "+ DAILY REVIEW" button
3. Record performance metrics, psychology rating, observations
4. Flag any mistakes using the mistake property on trades
5. Create a **Psychology Observation** if emotional state impacted trading

### Weekly

1. Create a **Weekly Review** via QuickAdd
2. Review all daily reviews from the week
3. Analyse performance by regime, asset, session
4. Update strategy notes if new rules or modifications identified
5. Create **Research Experiments** for hypotheses that arose

---

## STRATEGY EVOLUTION

The correct workflow for strategy changes:

1. Create a **Changelog** entry documenting the change
2. Create a new **Strategy Version** with updated rules
3. Update the Strategy master note [[STR-V6]] to point to the new version
4. Update [[System - Config]] with the new current version

---

## RESEARCH WORKFLOW

### Starting Research

1. Create a **Research Experiment** via QuickAdd
2. State a clear hypothesis
3. Define the method, sample size, and data period
4. Link relevant variables and market conditions

### Conducting Research

1. Record observations as you test
2. Link evidence (screenshots, data)
3. Update status to "In Progress" when actively testing

### Completing Research

1. Record results and conclusion
2. Set conclusion-type: CONFIRMED, REFUTED, INCONCLUSIVE, or PARTIAL
3. Update status to "Completed"
4. If confirmed, create a RULE note in Knowledge

---

## KNOWLEDGE MANAGEMENT

### Information Type Hierarchy

| Type | Description | Promotion Path |
|---|---|---|
| UNVERIFIED-IDEA | Raw idea, not evaluated | Test it |
| PERSONAL-OPINION | Subjective belief | Research it |
| OBSERVATION | Noticed phenomenon | Create experiment |
| HYPOTHESIS | Testable theory | Run experiment |
| EXPERIMENT | Active empirical test | Complete it |
| CONCLUSION | Result of experiment | Verify it |
| FACT | Objectively verifiable | Stable |
| RULE | Confirmed, tested trading rule | Stable |

### Knowledge Notes

- Notes with information-type = RULE are stored in `07-Knowledge/Rules/`
- All other knowledge notes are stored in `07-Knowledge/Concepts/`
- Notes can be promoted by changing their `information-type` and moving them

---

## QUICKADD COMMANDS

| # | Command | Creates |
|---|---|---|
| 01 | New Trade | Trade note in `01-Journal/Trades/YYYY/` |
| 02 | New Session | Session note in `01-Journal/Sessions/YYYY/` |
| 03 | Daily Review | Review note in `01-Journal/Reviews/YYYY/` |
| 04 | Weekly Review | Review note in `01-Journal/Reviews/YYYY/` |
| 05 | New Strategy | Strategy note in `02-Strategies/Registry/` |
| 06 | New Strategy Version | Version note in `02-Strategies/Versions/` |
| 07 | New Changelog | Changelog note in `02-Strategies/Changelogs/` |
| 08 | New Research | Experiment note in `03-Research/Experiments/` |
| 09 | New Backtest | Backtest note in `03-Research/Backtests/` |
| 10 | New Observation | Observation note in `03-Research/Observations/` |
| 11 | New Mistake | Mistake note in `06-Psychology/Mistakes/` |
| 12 | New Psychology | Psychology note in `06-Psychology/Observations/` |
| 13 | New Evidence | Evidence note in `08-Evidence/` |
| 14 | New Asset | Asset note in `04-Market/Assets/` |
| 15 | New Variable | Variable note in `05-Variables/` |
| 16 | New Knowledge | Knowledge note in `07-Knowledge/Rules/` or `Concepts/` |

---
*[[DATA DICTIONARY|Data Dictionary]]* | *[[WORKFLOW GUIDE|Workflow Guide]]* | *[[Dashboard - Trading OS|Home]]*