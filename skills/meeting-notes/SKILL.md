# Meeting Notes

## Trigger
Raw notes posted directly, voice transcription provided, or "process my notes from [meeting]" / "grab my notes from [Notion/Confluence] for [account]".

## Steps

### From Raw Notes or Transcription
1. Identify account name, date, attendees from the content.
2. Structure into the output format below.
3. Separate action items: MY items vs CUSTOMER items. Owner + due date on each.
4. Flag any risk signals: churn language, competitor mentions, frustration, escalation requests, feature blockers.
5. Save to `accounts/{account-name}/meeting-notes/YYYY-MM-DD-{topic}.md`. Create the folder if it doesn't exist.
6. Update main account file `accounts/{account-name}.md`:
   - Update last contact date
   - Add meeting reference to `<details>` dropdown section
   - Update any key relationship notes
7. Update `tracking/waiting-on.md` with new customer action items.
8. Update `tracking/to-do.md` with new MY action items.
9. If account file doesn't exist, create it from `accounts/_template.md`.

### From Notion / Notes Tool
1. Search your notes system — use broad keywords (e.g. "Acme renewal" not exact title).
2. If nothing returned, try shorter search term.
3. Fetch full page content.
4. Read the full content before doing anything else.
5. Run steps 1–9 above on the fetched content.
6. Write structured summary back to the original page.

---

## Output Format

```
## Meeting Notes: {Account Name}
**Date:** {date}
**Attendees:** {names + roles}
**Type:** {check-in / onboarding / QBR / escalation / ad-hoc}

### Key Decisions
- {decision with context}

### My Action Items
- [ ] {item} — due {date}

### Customer Action Items
- [ ] {item} — {owner} — due {date}

### Risk Signals
{churn indicators, competitor mentions, frustration, blockers — or "None identified"}

### Notes
{feature requests, product feedback, relationship context, anything worth keeping}
```

---

## Rules
- Never append meeting notes to the main account file. Always use the nested folder.
- Always separate MY vs CUSTOMER action items.
- Flag risk signals even if minor — easier to clear them than miss them.
- If notes search returns nothing on first try, use a shorter/broader term before giving up.
- Write back to your notes tool after processing — close the loop.
