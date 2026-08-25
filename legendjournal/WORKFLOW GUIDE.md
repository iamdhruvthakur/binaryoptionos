# WORKFLOW GUIDE

> Practical workflows for common tasks in the Trading OS.

---

## DAILY TRADING WORKFLOW

### 1. Session Start
- Open [[Dashboard - Trading OS|Home Dashboard]]
- Use "+ NEW SESSION" button to create today's session
- Select the session type (London, New York, etc.)
- Select the market regime
- Note your mental state and market bias

### 2. Taking Trades
- Use "+ NEW TRADE" button for each trade
- Select the asset, direction, and result
- After the trade, fill in:
  - Trade Context
  - Setup Description (check the variable checklist)
  - Entry Analysis
  - Post-Trade Analysis
  - Link evidence screenshots

### 3. End of Day
- Complete the session note with summary
- Use "+ DAILY REVIEW" to create a review
- Record: total trades, wins, losses, psychology rating
- Identify any mistakes
- Note what went well and what to improve

---

## WEEKLY REVIEW WORKFLOW

### 1. Create Weekly Review
- Use QuickAdd command 04 (Weekly Review)
- It auto-generates the week number and year

### 2. Review the Week
- Link all daily reviews from the week
- Fill in performance by regime table
- Review by asset and variable
- Identify recurring mistakes

### 3. Strategy Assessment
- Note key discoveries
- Document any strategy adjustments needed
- Set goals for next week

---

## STRATEGY EVOLUTION WORKFLOW

### Adding a New Strategy Change

1. **Create Changelog** (QuickAdd 07)
   - Document what changed and why
   - Reference supporting evidence
2. **Create Strategy Version** (QuickAdd 06)
   - Document full rule set
   - Link to the changelog
3. **Update Strategy Master** ([[STR-V6]])
   - Update `current-version` property
   - Add new version to version history table
4. **Update System Config** ([[System - Config]])
   - Update `current-version`

---

## RESEARCH WORKFLOW

### Starting an Experiment

1. Use "+ NEW RESEARCH" or QuickAdd 08
2. Write a clear research question
3. State your hypothesis explicitly
4. Define: method, sample size, data period
5. Link relevant variables and conditions

### Running the Experiment

1. Update status to "In Progress"
2. Record observations in the Observations section
3. Add evidence as you go
4. When complete, document results

### Finishing

1. Write conclusion
2. Set `conclusion-type`: CONFIRMED / REFUTED / INCONCLUSIVE / PARTIAL
3. Update status to "Completed"
4. If CONFIRMED, create a RULE in Knowledge

---

## MISTAKE TRACKING WORKFLOW

### Identifying a Mistake

1. On the trade note, set the `mistake` property to link to a Mistake note
2. Set `psychology-flag: true` if psychology was involved
3. If the mistake type doesn't exist yet, create it via QuickAdd 11

### Reviewing Mistakes

1. Open [[Dashboard - Psychology|Psychology Dashboard]]
2. Review Mistake Frequency table
3. Check for recurring patterns
4. Update mistake resolution strategies

---

## EVIDENCE WORKFLOW

1. Take a screenshot of the chart
2. Create an Evidence note via QuickAdd 13
3. Paste or embed the image
4. Link it to the relevant trade, research, or observation
5. Add the evidence link to the parent note's `evidence` property

---

## KNOWLEDGE MANAGEMENT WORKFLOW

### Importing Knowledge

1. Create a Knowledge note via QuickAdd 16
2. Select the appropriate information-type
3. If it's a RULE, it goes to `07-Knowledge/Rules/`
4. Everything else goes to `07-Knowledge/Concepts/`

### Promoting Knowledge

- OBSERVATION or HYPOTHESIS can be promoted by:
  1. Creating a Research Experiment to test it
  2. If confirmed, create a new RULE note
  3. Archive or update the original note

---
*[[SYSTEM GUIDE|System Guide]]* | *[[DATA DICTIONARY|Data Dictionary]]* | *[[Dashboard - Trading OS|Home]]*