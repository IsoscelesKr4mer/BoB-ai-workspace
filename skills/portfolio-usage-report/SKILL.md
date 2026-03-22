# Portfolio Usage Report

## Trigger
"Portfolio usage report" / "usage report for all accounts" / "usage trends across my portfolio" / any request for usage data across multiple accounts.

## What This Does
Queries your analytics tool for key activity metrics for every account in your portfolio across four time windows: 12 months, 6 months, 3 months, 1 month. Produces a report with trends and action items.

## Before Starting
1. Read `tracking/product-analytics-hashes.md` — this is the account list. Only query accounts with identifiers. Note any missing.
2. Read `tracking/portfolio-summary.md` for current account context.
3. Read `skills/product-analytics/SKILL.md` for query syntax.

## Steps

1. **For each account with an identifier**, run queries for your key events across the four date windows:
   - Last 12 months
   - Last 6 months
   - Last 3 months
   - Last 1 month

2. **Record results** as you go. Don't accumulate in memory — note each account's numbers before moving to the next.

3. **Identify trends** for each account:
   - 📈 Growing: month-over-month increase
   - 📉 Declining: month-over-month decrease, especially sharp drops
   - ➡️ Flat: consistent usage, no significant change
   - ⚠️ Inactive: very low or zero activity in last 30 days

4. **Compile report** in the output format below.

5. Save output to `tracking/account-usage-report-{YYYY-MM}.md`.

## Output Format

```
# Portfolio Usage Report — {date}
**Period:** {start} to {end}
**Accounts:** {n} with analytics data

## Summary
{2–3 sentences: overall portfolio health, notable trends}

## Account Breakdown

| Account | 12mo [Event] | 6mo [Event] | 3mo [Event] | 1mo [Event] | 12mo Sessions | 6mo Sessions | 3mo Sessions | 1mo Sessions | Trend |
|---------|-------------|-------------|-------------|-------------|--------------|--------------|--------------|--------------|-------|

## Trend Analysis

### 📈 Growing
- **[Account]:** {specific observation + recommended action}

### 📉 Declining
- **[Account]:** {specific observation + recommended action — these are highest priority}

### ⚠️ Inactive / Low Usage
- **[Account]:** {observation — flag for outreach}

### ➡️ Stable
- **[Account]:** {brief note}

## Recommended Actions
1. {highest priority — usually declining or inactive accounts}
2. {renewal risk accounts with low usage}
3. {growth accounts worth celebrating or expanding}

## Accounts Missing Analytics Data
{list any accounts without identifiers — flag for manual lookup}
```

## Rules
- Process one account at a time. Don't batch in memory.
- Note missing identifiers but don't block — report on what you have.
- Action items from this report go in `tracking/to-do.md`.
- Declining usage at accounts with upcoming renewals = highest priority flag.
