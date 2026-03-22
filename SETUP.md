# Setup Guide

This guide takes you from zero to a working AI workspace tailored to your stack. The goal: a CS or sales professional with an Anthropic subscription, no engineering background required.

---

> ## The Most Important Thing in This Guide
>
> **If you get stuck, if something isn't working, or if you want to change how the workspace behaves — open Cowork, give it access to your workspace folder, and just describe the problem in plain English. Cowork will read the files, figure out what's wrong, and fix it for you.**
>
> You don't need to understand the file structure. You don't need to edit CLAUDE.md or skill files by hand. You don't need to know what a regression is or how MCP connectors work under the hood. Just tell Cowork what you want:
>
> *"The call prep briefings are too long — can you make them shorter?"*
> *"I want it to stop asking me to confirm the email address every time — I trust it."*
> *"The Salesforce queries aren't pulling my accounts — help me fix it."*
> *"I want to add a new skill that preps me for executive sponsor calls."*
>
> This is how the workspace is meant to be customized and maintained. The files are the configuration — Cowork is the interface for changing them. You never have to touch a text editor.

---

## What You Need

- **Anthropic subscription** — Claude Pro ($20/mo) works. Claude Max is better for heavy daily use since you'll be running multi-step workflows.
- **[Claude Cowork](https://claude.ai)** — the desktop app that runs this workspace. Currently in research preview; access is included with Claude Pro/Max.
- **The tools you already use** — CRM, analytics, email, notes. You don't need all of them on day one.

That's it. **95% of this workspace works out of the box with just Cowork** — call prep, meeting notes, email drafts, CRM sync, analytics queries, account health checks, all of it. Claude Code and Discord are optional additions for two specific things covered in Step 3, and you don't need to think about them to get started.

---

## Step 1: Get the Repo

```bash
git clone https://github.com/[your-username]/csm-ai-workspace.git
```

Or just download the ZIP from GitHub and unzip it somewhere sensible — your Documents folder, a work folder, wherever you keep things.

---

## Step 2: Open It in Cowork

1. Open the Claude desktop app
2. Start a new Cowork session
3. When prompted to select a folder, choose your `csm-ai-workspace` folder
4. Cowork now has read/write access to everything in that folder

That's the whole setup. The `CLAUDE.md` file is automatically loaded as the AI's operating instructions.

---

## Step 3: Add Claude Code + Discord (Nice to Have)

Skip this entirely if you want to get up and running fast. Everything in this repo works without it. Come back here once you've been using the workspace for a while and want to go deeper.

There are two specific things Cowork can't do that Claude Code unlocks:

**1. gog CLI for Gmail** — Cowork connects to Gmail via MCP connector, which covers reading, searching, and drafting. But the gog CLI is a purpose-built command-line tool for Gmail power users that goes significantly further: bulk label management, automated filter creation, Drive uploads, applying labels to threads, and more. It runs as bash commands in the terminal, which only Claude Code has access to. If you want this level of Gmail control — and it's genuinely useful once you have it — you need Claude Code.

**2. Always-on two-way communication via Discord** — Cowork requires you to be sitting at your computer with the app open. Claude Code running with a Discord integration means your workspace is always listening. You can message it from your phone mid-commute, between meetings, or from anywhere: *"Prep me for the Acme call in an hour"* and the briefing will be in your Discord channel before you sit down. It also means the AI can proactively post to you — renewal alerts, action item syncs, draft notifications — without you having to ask.

Everything else: call prep, meeting notes, email drafts, CRM sync, analytics queries, account health, portfolio reports — all of it works out of the box in Cowork alone.

### Installing Claude Code

```bash
npm install -g @anthropic/claude-code
```

Then authenticate:

```bash
claude login
```

This ties Claude Code to your Anthropic account — the same subscription you're already using for Cowork.

### Running Claude Code against your workspace

Navigate to your workspace folder in the terminal and launch Claude Code:

```bash
cd /path/to/csm-ai-workspace
claude
```

Claude Code reads `CLAUDE.md` automatically, just like Cowork does. Everything you've configured there applies in both interfaces.

### Setting up Discord integration

This is what lets you message the AI from Discord and have it respond in a channel — and lets the AI post action items, draft notifications, and portfolio alerts on its own.

**1. Create a Discord server** (or use one you already have). Create channels for the outputs you want:
- `#general` — action item syncs, portfolio alerts
- `#call-prep` — call prep briefings
- `#email-drafts` — drafts pending your approval
- `#meeting-notes` — processed meeting note outputs

**2. Install the Discord MCP for Claude Code.** In your Claude Code session:

```
claude mcp add discord
```

Follow the prompts to connect to your server and authenticate. You'll need to grant the bot access to the channels you created.

**3. Update CLAUDE.md** with your channel names so the AI knows where to post what. The Discord section is already in the template — just swap in your actual channel names.

**4. To message Claude Code from Discord:** The Discord MCP enables bidirectional communication. You post a message in a designated channel, Claude Code picks it up and responds. Useful for: *"Prep me for my Acme call at 2pm"* sent from your phone before you walk into the office.

### The Cowork + Claude Code hybrid

You'll likely end up using both:

- **Cowork** for most day-to-day work — it has a better UI for reading files, longer conversations, and easier MCP connector management.
- **Claude Code** (via Discord or terminal) for background tasks, terminal-dependent workflows (gog), and anything you want to kick off asynchronously.

Both read the same workspace folder. Files created or updated in one are immediately visible to the other. There's no sync to manage.

---

## Step 4: Customize CLAUDE.md for Your Stack

**This is just a framework.** The CLAUDE.md file and the skill files are a starting point — not a fixed system. Everything about how the AI behaves is defined in plain text files that you can change. The tone, the personality, the output formats, the rules, what it does automatically vs. what it asks permission for, how it handles emails, how long call prep briefings are — all of it is configurable, and none of it requires technical knowledge to change.

You can edit anything by telling Cowork what you want:

> *"Make the tone a little more formal — I work with enterprise legal and compliance teams."*
> *"Stop including a suggested agenda in call prep — I handle that myself."*
> *"I want email drafts to be shorter by default. Two paragraphs max."*
> *"Add a rule: always check if there's an open support ticket before drafting a customer email."*
> *"I prefer bullet points over paragraphs for meeting notes summaries."*

Cowork will read the relevant file, make the change, and show you what it updated. You can also just open `CLAUDE.md` or any skill file in a text editor and change it directly — it's markdown, nothing fancy.

The point is: if the workspace isn't behaving the way you want, that's not a limitation — it's just a config file that hasn't been updated yet.

---

To wire up your tools and integrations, tell Cowork:

> *"I'm an account manager at [Company]. I use Salesforce as my CRM, Amplitude for analytics, Gmail, and Confluence for notes. My name is [Name] and I'm based in [City]. Help me customize CLAUDE.md for my setup."*

The AI will read the current `CLAUDE.md`, ask you a few clarifying questions about your tools and workflow, and update the file for your stack. It can also update the skill files to reference your actual tool names.

**Things to tell it:**
- Your name, company, and role
- Your CRM (and if you know it, your owner/user ID in that CRM)
- Your analytics tool and what events matter most (key actions your customers take in your product)
- Your notes tool (Notion, Confluence, etc.)
- Your email client
- Any team communication tools (Slack, Discord, Teams)
- How you prefer to receive action items and summaries

---

## Step 5: Connect Your Tools

Cowork connects to external tools via **MCP connectors** — lightweight integrations that give the AI read (and sometimes write) access to your tools. You install them from within the app.

In Cowork, go to **Settings → Connectors** (or ask the AI: *"What connectors are available?"*). Below is a map of common CS/sales tools to their connectors.

### CRM

| Tool | Connector | What It Unlocks |
|------|-----------|-----------------|
| HubSpot | HubSpot MCP | Query companies, contacts, deals, meetings by owner |
| Salesforce | Salesforce MCP | Query accounts, opportunities, activity history |
| Pipedrive | Pipedrive MCP | Deals, contacts, pipeline stages |
| Attio | Attio MCP | Companies, contacts, lists |
| Zoho CRM | Zoho MCP | Accounts, deals, activities |

**After connecting your CRM:** Update the CRM section of `CLAUDE.md` with your actual owner/user ID and your custom field names. Your CRM's internal field names are often different from the display names — HubSpot and Salesforce especially. Ask the AI: *"Pull my HubSpot properties and show me the internal API names for ARR and renewal date."* It can look these up and update CLAUDE.md for you.

### Product Analytics

| Tool | Connector | Notes |
|------|-----------|-------|
| Mixpanel | Mixpanel MCP | Events, user properties, insights queries |
| Amplitude | Amplitude MCP | Charts, user lookup, event volumes |
| Heap | Heap MCP | Session data, event counts |
| Pendo | Pendo MCP | Feature adoption, NPS, guide views |
| Gainsight PX | Gainsight MCP | Engagement scores, feature usage |
| Segment | Segment MCP | Raw event data, trait queries |

**The customer identifier problem:** Every analytics tool stores customers under some ID — sometimes a hashed value, sometimes an account name, sometimes a domain. The `tracking/product-analytics-hashes.md` file is where you keep the mapping between account name and that identifier. Fill it in as you go; the AI will prompt you when it hits an account it doesn't have an ID for.

**What events to track:** Update `skills/product-analytics/SKILL.md` with the events that signal engagement in your product. Think: what does a healthy, active customer do regularly? That's your primary event. What signals someone logging in? That's your session event. Two events is enough to start.

### Email & Calendar

| Tool | Connector |
|------|-----------|
| Gmail | Gmail MCP |
| Google Calendar | Google Calendar MCP |
| Outlook / Microsoft 365 | Microsoft 365 MCP |

The email drafter skill creates drafts directly in your drafts folder — it never sends. You review, edit if needed, send yourself.

### Notes & Documentation

| Tool | Connector | Notes |
|------|-----------|-------|
| Notion | Notion MCP | Full read/write — ideal for meeting notes (see below) |
| Confluence | Confluence MCP | Read meeting pages, search by account name |
| Obsidian | Local file access | Already works if your vault is in the workspace folder |
| Google Docs / Drive | Google Drive MCP | Read docs, search by name |

### Team Communication

| Tool | Connector | Use Case |
|------|-----------|----------|
| Slack | Slack MCP | Post action items to a channel, get notified on updates |
| Discord | Discord MCP | Same as Slack — good for solo operators or small teams |
| Microsoft Teams | Teams MCP | Enterprise alternative |

**Setting up a Slack or Discord workflow:** Connect the MCP, then tell the AI which channels to use for which outputs (action items, email drafts pending review, portfolio alerts, etc.). Update the relevant section of `CLAUDE.md` with those channel names. The skill files reference Discord by default — the AI can update them to Slack with one instruction.

### Customer Success Platforms

If your company uses a dedicated CS platform, check for an MCP before falling back to CRM data alone.

| Tool | Notes |
|------|-------|
| Gainsight | Health scores, CTAs, timeline notes |
| ChurnZero | Segments, health scores, usage scores |
| Totango | SuccessPlays, health metrics |
| Vitally | Projects, health scores, notes |

These tools often have the best pre-built health scoring. If you have one, the account-health skill can incorporate that score directly rather than computing from raw renewal dates and analytics data.

---

## Step 6: The Notion Meeting Workflow

This is the highest-leverage workflow in the whole system. Here's how it works end to end.

### Recording the meeting

Notion has a built-in AI meeting recorder (Notion AI add-on). During your customer call:

1. Open a new Notion page in your customer's workspace section
2. Click **+ → Meeting recording** (or use the `/meeting` command)
3. Start recording — Notion transcribes in real time
4. When the call ends, stop the recording

Notion AI will automatically generate a summary with action items. That's your raw material.

**Don't have Notion AI?** Any of these work the same way — just paste the transcript or notes into a Notion page:
- **Otter.ai** — records and transcribes, exports full transcript
- **Fireflies.ai** — similar, integrates directly with Google Meet / Zoom
- **Fathom** — good free tier, auto-generates summaries
- **Zoom AI Companion** — if your company uses Zoom, this is built in
- **Google Meet transcription** — available in Workspace plans

The format doesn't matter much. A raw transcript, a bulleted summary, a voice memo you typed up — the AI can work with all of it.

### Getting the AI to process it

Once the notes are in Notion, just say:

> *"Grab my notes from today's call with Acme and process them."*

The AI will:
1. Search Notion for a recent page matching that account name
2. Fetch the full content
3. Structure it into the standard format (decisions, my action items, customer action items, risk signals, notes)
4. Save the structured notes to `accounts/acme/meeting-notes/YYYY-MM-DD-topic.md`
5. Update the main Acme account file with the last contact date and a reference to the new notes
6. Add action items to `tracking/to-do.md` and `tracking/waiting-on.md`
7. Write the structured summary back to the Notion page

You end up with the notes filed in two places (your workspace + Notion), action items tracked, and the account file updated — from one sentence.

### Or just paste the notes directly

If you don't use Notion, just paste raw notes into the chat:

> *"Here are my notes from today's FanDuel call: [paste notes]"*

Same output. The Notion step is optional — it just means the AI can pull them without you having to copy-paste.

---

## Step 7: Gmail Organization with gog CLI

> **Requires Claude Code.** gog is a command-line tool — it runs as a bash command in Claude Code's terminal. Cowork doesn't have terminal access, so gog commands won't work there. Set up Claude Code first (Step 3), then come back here.
>
> Once Claude Code is running, you can trigger gog workflows from the terminal, from a Claude Code session, or by messaging your Discord channel: *"Apply the Escalations label to the thread from Sarah at Acme."*

The `gog` CLI handles Gmail label management, filter creation, and Drive uploads — things the Gmail MCP can't do. If you're running this workspace daily, a clean inbox structure makes a real difference.

### Installing gog

```bash
# macOS
brew install gog

# Or download from https://github.com/[gog-repo]
```

Once installed, authenticate:

```bash
gog auth login -a your.email@company.com
```

### Label setup

A clean label structure keeps customer threads findable without manual sorting:

```bash
# Create your core labels
gog gmail labels create -a your.email@company.com "Customers"
gog gmail labels create -a your.email@company.com "Customers/Renewals"
gog gmail labels create -a your.email@company.com "Customers/Escalations"
gog gmail labels create -a your.email@company.com "AI Drafts"
gog gmail labels create -a your.email@company.com "Needs Reply"
```

### Filters

Automatically label incoming mail from customer domains:

```bash
# Label all mail from a customer domain
gog gmail filters create -a your.email@company.com \
  --from "@acmecorp.com" \
  --add-label "Customers"

# Flag renewal-related subjects
gog gmail filters create -a your.email@company.com \
  --subject "renewal" \
  --add-label "Customers/Renewals"
```

The AI can help you build a filter list from your account files:

> *"Look at my accounts folder and generate gog filter commands for all my customer domains."*

It will read each account file, pull the contact email domains, and output a ready-to-run script.

### Using gog in the workflow

The AI uses gog for things the Gmail MCP can't do:

- **After creating a draft:** optionally apply the "AI Drafts" label so you can find all pending drafts quickly
- **Uploading reports to Drive:** `gog drive upload -a your.email@company.com report.xlsx`
- **Listing calendars:** `gog calendar list -a your.email@company.com` — useful for confirming which calendar to check for upcoming customer calls
- **Applying labels to threads:** `gog gmail thread modify -a your.email@company.com [threadId] --add "Customers/Escalations"`

You don't need to learn gog commands yourself — the AI handles the syntax. But you do need it installed and authenticated for these workflows to work.

---

## Step 8: First Run Checklist

Once everything is connected, run through this to confirm the basics are working:

**CRM sync:**
> *"Sync my accounts from [CRM] and update my portfolio summary."*

This should populate `tracking/portfolio-summary.md` with your real accounts and ARR data. If it fails, check that your owner/user ID in `CLAUDE.md` is correct.

**Account file:**
> *"Create an account file for [one of your accounts]."*

Should create `accounts/account-name.md` using data from your CRM. If the file is mostly blank, your CRM field names in `CLAUDE.md` might need adjusting.

**Call prep:**
> *"Prep me for a call with [account]."*

Tests CRM lookup, analytics query, open items check, and web search in one shot. A good end-to-end smoke test.

**Email draft:**
> *"Draft a quick check-in email to [contact name] at [account]."*

Should ask you to confirm the email address, then produce a draft that doesn't sound corporate.

---

## Tips

**Start with one workflow.** Call prep is the highest immediate value — you feel the difference on the first call. Get that working before adding more connectors.

**The account files compound.** The more context is in `accounts/{name}.md`, the better every workflow gets. After each meeting, file the notes. After each call prep, add any new context you learned. Over a few weeks, the AI knows these accounts almost as well as you do.

**Add regressions as you go.** When the output isn't quite right, add a one-line fix to the relevant skill file. It's the difference between a workspace that plateaus and one that keeps improving.

> *"Add a regression to the email-drafter skill: [what went wrong → rule that prevents it]."*

**Customize the humanizer.** The kill list is opinionated. If your customers are more formal, or if you use certain phrases intentionally, edit `skills/humanizer/SKILL.md` to reflect your actual voice. The goal is that a reader can't tell the AI helped — it should sound like you.

**You can ask the AI to improve itself.** If a skill output isn't matching what you want, describe the gap:

> *"The call prep briefings are too long. Update the call-prep skill to aim for half the length."*

It will read the skill file and propose an edit. This is how the workspace evolves without requiring you to understand the underlying structure.

---

## Troubleshooting

**Before reading any of this:** open Cowork, point it at your workspace folder, and describe what's broken. Nine times out of ten it'll find and fix the issue faster than following a troubleshooting guide. The specific scenarios below are here if you want to understand *why* something failed, not because you need them to fix it.

**"The AI doesn't know my account."**
The account file probably doesn't exist yet. Ask it to create one from CRM data, or run the CRM portfolio sync.

**"CRM queries are returning nothing."**
Usually a field name mismatch. Ask: *"Check my CLAUDE.md CRM field names against what's actually in HubSpot/Salesforce."* The AI can query your CRM's property list and spot the discrepancy.

**"Analytics queries return no data."**
The customer identifier is probably wrong or missing. Check `tracking/product-analytics-hashes.md`. If the account is listed, the identifier may have changed — look it up in the analytics tool's Users tab and update the file.

**"The email sounds like an AI wrote it."**
Run the humanizer explicitly: *"Re-run humanizer on that draft."* If it keeps happening, add a regression to `skills/humanizer/SKILL.md` capturing what the specific issue was.

**"The AI is doing things I didn't ask."**
Check `CLAUDE.md` trust boundaries. External actions (sending, posting) should always require approval. If that section got modified, restore it.
