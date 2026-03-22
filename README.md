# BoB — Book of Business AI Workspace

An AI workspace for anyone who owns a book of business — CS, sales, account management, and partnerships. Built for Claude (via [Cowork](https://claude.ai) or [Claude Code](https://docs.claude.com/en/docs/claude-code/overview)), but adaptable to any AI tool that supports a system prompt or instruction file.

---

## Meet BoB

BoB is the name for your AI assistant in this workspace — short for Book of Business. You can rename it to whatever you want in `CLAUDE.md`. Some people name theirs after a favorite colleague. Some keep it generic. BoB is just a starting point.

---

## What This Is

Most people who experiment with AI for account work end up with a generic chatbot that doesn't know their accounts, can't prep for a specific call, and produces emails that sound like they were written by a consultant. This workspace fixes that.

The core idea: treat the AI as a specialized team member with its own operating procedures, not a search box. Give it structure, context, and a clear chain of custody for information. Get results that are actually useful.

**What this workspace does:**
- Preps you for customer calls with live CRM data, usage trends, open items, and relevant news — in one briefing
- Processes raw meeting notes into structured output with separated action items (yours vs. the customer's)
- Drafts customer emails that don't sound like corporate templates
- Tracks your portfolio's renewal risk and usage health
- Maintains a persistent knowledge base that gets smarter over time

---

## Philosophy

**Context is everything.** An AI that doesn't know your accounts is a generic tool. An AI that knows your portfolio, your customers' renewal dates, their usage trends, and your open action items is an actual assistant.

**Skills over one-shot prompts.** Each workflow is a skill file — a short document that defines triggers, steps, output format, and rules. The AI reads the relevant skill before executing. This means consistent, repeatable outputs that you can improve over time.

**Separation of concerns.** Internal notes and customer-facing content are handled differently. The humanizer runs automatically on everything that goes to a customer. Trust boundaries are explicit: the AI drafts, you approve.

**Learning by regression.** When something goes wrong, you add a one-line rule to the relevant file. Over time, the workspace gets more reliable, not less.

---

## Folder Structure

```
bookofbusiness-ai-workspace/
├── CLAUDE.md                         ← Main instruction file (configure this first)
│
├── skills/                           ← Workflow modules
│   ├── call-prep/SKILL.md            ← Pre-call briefings
│   ├── meeting-notes/SKILL.md        ← Note processing + filing
│   ├── email-drafter/SKILL.md        ← Email drafts + inbox triage
│   ├── humanizer/SKILL.md            ← Anti-corporate prose rules
│   ├── account-health/SKILL.md       ← Risk scoring (single + portfolio)
│   ├── crm-portfolio-sync/SKILL.md   ← Pull CRM data → update files
│   ├── product-analytics/SKILL.md    ← Usage queries
│   └── portfolio-usage-report/SKILL.md ← Cross-account usage trends
│
├── accounts/                         ← One file per customer (auto-populated from CRM)
│   └── _template.md                  ← Reference only — BoB generates these from your CRM
│
├── tracking/                         ← Always-on operational files
│   ├── portfolio-summary.md          ← Canonical portfolio view (auto-generated)
│   ├── to-do.md                      ← Your open action items
│   ├── waiting-on.md                 ← Customer open action items
│   ├── renewal-pipeline.md           ← Active renewal tracking
│   └── product-analytics-hashes.md  ← Customer → analytics identifier map
│
└── memory/                           ← Daily logs
    ├── YYYY-MM-DD.md                 ← Today's log (auto-created)
    └── archive/                      ← Logs >30 days old
```

---

## Setup

**Full setup guide with connector options, Notion meeting workflow, Gmail organization, and Cowork customization:** [SETUP.md](./SETUP.md)

**Real-world use cases with example prompts:** [USE-CASES.md](./USE-CASES.md)

> **Stuck or want to customize something?** Open Cowork, give it access to your workspace folder, and describe what you want in plain English. It will read the files and fix or change whatever you need — no manual editing required. This is the intended workflow for customization and troubleshooting.

### Quick start

### 1. Configure CLAUDE.md

Open `CLAUDE.md` and replace every `[BRACKETED PLACEHOLDER]` with your information:

- **Your name and role** — the AI needs to know who it's working for
- **Your CRM owner ID** — so it can query your accounts (not someone else's)
- **Your CRM field names** — HubSpot custom field names are shown; adjust for your CRM
- **Your analytics tool** — Mixpanel examples are included; adapt to Amplitude, Heap, etc.
- **Your integrations** — remove sections for tools you don't use (Notion, Discord, etc.)

### 2. Connect your tools (MCPs)

This workspace is built to work with MCP (Model Context Protocol) connectors. In Cowork or Claude Code, install connectors for:

- **CRM** — HubSpot, Salesforce, etc.
- **Product analytics** — Mixpanel, Amplitude, etc.
- **Email** — Gmail, Outlook
- **Calendar** — Google Calendar, etc.
- **Notes** — Notion, Confluence (optional)

The skill files reference generic tool names. Update the tool name comments in each skill file to match your actual MCP connector names once connected.

### 3. Add your accounts

Just tell BoB to pull your accounts from your CRM:

> *"Sync my accounts from HubSpot and create account files for each one."*

That's it. BoB will query your CRM, pull contract and contact data for every account you own, and build out the `accounts/` folder automatically. The `accounts/_template.md` file is just there as a reference for what an account file looks like — you don't need to touch it.

### 4. Start using it

Drop the workspace folder where your AI tool can read it (Cowork mounts it automatically). Then just talk to it:

- *"Prep me for my call with Acme tomorrow"*
- *"Process my notes from today's FanDuel QBR"*
- *"Draft a follow-up to Sarah at Acme re: the feature request"*
- *"Health check across my whole portfolio"*
- *"Pull usage data for all accounts — last 30 days"*

---

## Customizing the Humanizer

The humanizer (`skills/humanizer/SKILL.md`) is opinionated. It's tuned for a direct, warm voice that doesn't sound like a press release. If your communication style is different, edit the kill list and tone target to match. The important thing is that it runs automatically on every customer-facing draft — not just when you remember.

---

## The Regression Pattern

When something goes wrong, add a line to the relevant skill or CLAUDE.md:

```
[YYYY-MM-DD] What happened → rule that prevents it.
```

Example: `[2026-03-04] Em dashes appeared in email draft → scan full draft for "—" before presenting.`

This is the main way the workspace improves over time without any code changes.

---

## What's Not Included

- **Actual account data** — intentionally stripped. This is a template.
- **MCP connector setup** — varies by tool and AI client. See your AI client's documentation.
- **Discord/Slack integration** — the original workspace posts to Discord. That's optional and easy to add if you want it; the skill files reference it but the core workflows work without it.

---

## Built With

- [Claude](https://claude.ai) — Anthropic's AI
- [Cowork](https://claude.ai) — Claude desktop mode (where this was built and used daily)
- [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) — alternative Claude interface
- MCP connectors for HubSpot, Mixpanel, Gmail, Google Calendar, Notion

---

## Questions / Contributing

This is a working system, not a polished product. If you own a book of business and you adapt it to your stack, I'd be curious what you changed.
