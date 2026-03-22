# Account Health

## Trigger
"Account health check for [account]" / "how is [account] doing?" / "risk check for [account]" / "health score for my portfolio" / any request for risk assessment across one or all accounts.

## What This Does
Produces a structured health assessment combining renewal timeline, usage trends, open items, and relationship signals. Different from call-prep — this is a risk score, not a meeting brief.

## Single Account Health Check

1. **Load account file** — `accounts/{account-name}.md`. Note contract ARR, renewal date, key contacts.
2. **Renewal risk** — pull from `tracking/portfolio-summary.md`. Apply flag:
   - 🔴 OVERDUE — past renewal date
   - 🔴 HIGH — <30 days
   - ⚠️ MEDIUM — 31–90 days
   - ✅ LOW — >90 days
3. **Usage trend** — if identifier exists in `tracking/product-analytics-hashes.md`, query your analytics tool:
   - Pull key activity metrics for last 30 days and last 90 days
   - Compute trend: growing / flat / declining / inactive
   - Declining usage + near renewal = highest risk combination
4. **Open items** — scan `tracking/waiting-on.md` and `tracking/to-do.md` for account mentions. Flag anything overdue.
5. **Relationship signals** — check `memory/` files for the past 14 days for mentions. Note any churn language, escalation, or competitor references.
6. **Score and output.**

## Portfolio Health Check

Triggered by "health check for all accounts" / "portfolio risk review" / "where are my biggest risks?".

1. Load `tracking/portfolio-summary.md` — use as base.
2. Load `tracking/waiting-on.md` and `tracking/to-do.md` — flag accounts with overdue items.
3. Pull usage analytics for all accounts with identifiers (last 30 days).
4. Cross-reference: accounts with both ⚠️ renewal risk AND declining usage = critical.
5. Output portfolio risk table sorted by combined risk score.

---

## Output Format — Single Account

```
## Account Health: {Account Name}
**Date:** {today}
**Health Score:** 🔴 HIGH RISK / ⚠️ MEDIUM / ✅ LOW RISK

### Renewal
- ARR: ${amount}
- Renewal: {date} — {days} days out
- Status: {flag}

### Usage (last 30 days)
- {Key metric}: {n} | {Key metric 2}: {n}
- Trend: {📈 Growing / ➡️ Flat / 📉 Declining / ⚠️ Inactive}
- vs. prior 90 days: {comparison}

### Open Items
- {any overdue items from waiting-on or to-do — or "None"}

### Relationship Signals
- {recent memory mentions, risk language, or "Nothing flagged in last 14 days"}

### Assessment
{2–3 sentences: overall risk narrative, what needs to happen}

### Recommended Actions
1. {most urgent action}
2. {secondary action}
```

---

## Output Format — Portfolio

```
## Portfolio Health Check
**Date:** {today}

### Critical (renewal risk + declining usage)
| Account | ARR | Renewal | Usage Trend | Open Items |
|---------|-----|---------|-------------|------------|

### High Risk (overdue or <30 days)
| Account | ARR | Renewal | Usage Trend |

### Medium Risk (<90 days)
| Account | ARR | Renewal | Usage Trend |

### Low Risk (>90 days)
| Account | ARR | Renewal | Usage Trend |

### Summary
{Overall portfolio narrative — where is attention needed most?}

### Top 3 Actions
1. {highest urgency}
2.
3.
```

---

## Rules
- Always pull live usage data — don't rely on cached trends.
- Declining usage + upcoming renewal = always flag as critical regardless of days-out.
- If analytics identifier is missing, note it but don't block — score based on renewal + open items only.
- For portfolio view, process one account at a time — don't batch in memory.
- This skill produces a risk assessment, not a meeting brief. For meeting prep, use call-prep.
