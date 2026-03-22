# CRM Portfolio Sync

## Trigger
"Sync my accounts from [CRM]" / "update ARR for all accounts" / "pull renewal dates" / "refresh my portfolio data".

## What This Does
Queries your CRM for all accounts you own, pulls ARR and renewal data for each, updates account files, and regenerates `tracking/portfolio-summary.md`.

## Steps

1. **Get live account list** — always query fresh, never use a hardcoded list:
   ```
   Query your CRM for all companies where owner = [YOUR_OWNER_ID]
   Properties: name, id
   ```

2. **For each account returned**, pull full details:
   ```
   Properties: name, [arr_field], [next_renewal_field], [true_renewal_field], products, [other relevant fields]
   ```

3. **Analytics verification** — for each account, attempt to confirm their identifier in your analytics tool:
   - If confirmed: record in `tracking/product-analytics-hashes.md`.
   - If not found: note it — manual lookup may be needed.

4. **Update account file immediately** after each query — don't accumulate. Report each account as you go.

5. **Effective renewal date logic** — critical for multi-year contracts:
   - If your contract-end date field is populated → that is the **effective renewal date**. Use it for status flags, risk assessment, and sorting. The annual payment date on multi-year deals is NOT the contract end.
   - If that field is null → fall back to the annual renewal date field.
   - Never treat an annual payment milestone on a multi-year deal as an upcoming renewal risk.

6. **If a field returns null**, report it — don't silently carry forward stale data.

7. **After all accounts**, rewrite `tracking/portfolio-summary.md` with the format below.

---

## Portfolio Summary Format

```markdown
# Portfolio Summary — {date}
**CRM Data Refreshed:** {datetime}

## Total Portfolio
- **Total ARR:** ${sum}
- **{n} Active Accounts**

## All Accounts

| Account | ARR | Next Renewal | True Renewal | Status |
|---------|-----|--------------|--------------|--------|
| ...     |     |              |              |        |

## Risk Flags
{overdue, <30d, <90d, null data}
```

**Sort order:** By effective renewal date ascending (soonest first).
**Status flags:** 🔴 OVERDUE / ⚠️ <30 days / ⚠️ <90 days / ✅ — applied against effective renewal date.
**ARR total:** Always compute by summing line items. Never copy from previous version.

---

## Rules
- Process one account at a time — don't batch in memory.
- Save to account file before moving to next account.
- If any query fails, stop and report the error. Do not silently skip.
- Use `edit` for existing files, `write` only for new files.

## Regressions
- [YYYY-MM-DD] ARR total must be computed fresh every sync — never copied from previous version.
- [YYYY-MM-DD] Null fields must be reported, not silently skipped.
- [YYYY-MM-DD] Multi-year accounts: effective renewal date is the contract end field, not the annual payment date. Never flag the annual payment date as a renewal risk on multi-year deals.
