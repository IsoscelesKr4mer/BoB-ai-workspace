# Call Prep

## Trigger
"Prep me for my call with [account]" / "call prep for [account]" / account name mentioned ahead of a meeting.

## Steps

1. **Account file** — load `accounts/{account-name}.md`. If it doesn't exist, say so and offer to pull from CRM.
2. **Recent memory** — check `memory/YYYY-MM-DD.md` for the past 7 days for any mentions of this account.
3. **Open items** — check `tracking/waiting-on.md` and `tracking/to-do.md` for items tied to this account.
4. **Renewal status** — check `tracking/renewal-pipeline.md` and `tracking/portfolio-summary.md`.
5. **Live CRM data** — pull latest ARR, renewal date, last meeting date from your CRM.
6. **Recent CRM activity** — pull meetings/notes associated with the company from the last 90 days. Strip boilerplate — extract only substantive notes (decisions, concerns, context). Skip if nothing meaningful.
7. **Product analytics usage** — if customer identifier exists in `tracking/product-analytics-hashes.md`, pull last 30 days of key activity. Flag any notable trends (spike, drop, flat).
8. **Docs / Notes tool** — search for recent meeting notes or docs in your notes system (Notion, Confluence, etc.) with account name.
9. **Web search** — 1–2 targeted searches for recent news: "[Company] news [current year]", "[Company] + industry keyword". Include only genuinely relevant results.
10. **Compile briefing.**

---

## Output Format

```
## Call Prep: {Account Name}
**Date:** {today}
**Contact:** {primary contact name + role}
**Meeting type:** {check-in / QBR / renewal / onboarding / ad-hoc}

### Account Context
{2–3 sentences: what they do, how they use your product, contract overview}

### Renewal Status
{date, ARR, risk level — 🔴 overdue / ⚠️ <30d / ⚠️ <90d / ✅}

### Usage (last 30 days)
{key activity metrics, notable trends}

### Open Items
- {items from waiting-on.md with dates, flag anything overdue}

### Recent News
- {relevant company news, one-line each — skip if nothing meaningful}

### Suggested Agenda
1. {based on open items}
2. {based on renewal status or usage trends}
3. {based on recent news or relationship context}
```

---

## Rules
- Always pull live CRM data — don't rely solely on the account file for renewal dates or ARR.
- Only include web news if it's actually relevant. Don't pad the briefing with noise.
- If analytics identifier isn't in the file, note it and move on — don't block the rest of the prep.
- If account file doesn't exist, flag it and build from CRM data.
