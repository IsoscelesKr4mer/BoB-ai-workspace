# Email Drafter

## Trigger
Any request to draft, write, or send a customer-facing email.

## Two Modes

**Mode 1 — Standalone draft:** Describe the situation, recipient, and what needs to happen. Draft from context.

**Mode 2 — Inbox scan:** "Check my inbox" or "scan my email" — pull recent threads, cross-reference account files, present a prioritized list. Pick which get drafts.

---

## Mode 1 — Standalone Draft

1. Confirm recipient full name and email address before starting. Never guess. "Sending to [Name] at [email] — correct?"
2. Pull `accounts/{account-name}.md` for context if it exists.
3. Check `tracking/waiting-on.md` for relevant open items.
4. Check `tracking/to-do.md` for any outstanding action items tied to this account.
5. Draft the email.
6. **Run humanizer** — apply all rules from `skills/humanizer/SKILL.md`. This step is automatic and mandatory.
7. Create draft in your email client — goes directly into drafts folder.
8. Do not send. Ever. Without explicit approval.

## Mode 2 — Inbox Scan

1. Search recent unread emails.
2. For each thread, cross-reference sender domain against account files for context.
3. Present numbered priority list:
   ```
   1. [Sender] — [Subject] — [Urgency: high/medium/low] — [Account context if any]
   2. ...
   ```
4. Wait for direction on which get drafts.
5. Draft selected emails one at a time.
6. Run humanizer on each.
7. Create drafts in email client.

---

## Output Format

```
**To:** [full name] <email@domain.com>
**Subject:** [subject line]

[email body]
```

## Humanizer Checklist (run on every draft)
- [ ] No em dashes
- [ ] No "I hope this email finds you well" or equivalent
- [ ] No "please don't hesitate to reach out"
- [ ] No "certainly" / "absolutely" openers
- [ ] No leverage, streamline, delve, aligned, synergy
- [ ] No performed authenticity or hedging stacks
- [ ] Reads like a human CSM: direct, warm, specific

## Rules
- NEVER guess email addresses. Always confirm first.
- NEVER send without explicit approval.
- Humanizer is not optional. Apply it before every presentation.
- If account file doesn't exist for the recipient, note it and offer to create one.

## Regressions
- [YYYY-MM-DD] Em dashes found in final drafts. Scan the whole draft before presenting. Every time.
- [YYYY-MM-DD] Humanizer skipped under time pressure. It is not optional. It runs on every draft.
