# Product Analytics

## Trigger
Any request involving usage data, engagement metrics, activity trends, or account activity in your product analytics tool (Mixpanel, Amplitude, etc.).

## Before Any Query
Check `tracking/product-analytics-hashes.md` for the customer's identifier. If your analytics tool uses hashed or obfuscated customer IDs, plaintext names may silently return no data.

Identifier not in the file? Ask [YOUR NAME] to look it up in the analytics tool's Users/People tab. Save it to the hashes file once provided.

## Project / Workspace Setup
- **Project ID / Workspace:** `[YOUR_PROJECT_ID]`
- **Tool:** `[your analytics MCP tool name]`

## Query Structure

Adapt this to your analytics tool's API. Mixpanel example:

```json
{
  "project_id": "[YOUR_PROJECT_ID]",
  "report_type": "insights",
  "report": {
    "metrics": [
      {
        "eventName": "[YOUR_KEY_EVENT]",
        "measurement": {"type": "basic", "math": "total"}
      }
    ],
    "name": "{Customer} {Event} Report",
    "dateRange": {
      "type": "absolute",
      "from": "YYYY-MM-DD",
      "to": "YYYY-MM-DD"
    },
    "filters": [
      {
        "type": "string",
        "propertyName": "[CUSTOMER_IDENTIFIER_PROPERTY]",
        "operator": "equals",
        "value": "{identifier}",
        "resource": "user"
      }
    ]
  }
}
```

## Key Events to Track
<!-- Replace these with your product's actual events -->
- Primary engagement event: `[e.g., "Clip", "Export", "Report Generated"]`
- Session/login event: `[e.g., "$session_start", "Login", "App Open"]`
- Other key events: `[list your high-value events]`

## Rules
1. Filters go INSIDE the report/query object — not at the top level.
2. Always use the correct customer identifier type (hashed vs. plaintext).
3. Hash/identifier value must match exactly what's stored — case sensitive.
4. For portfolio reports across all accounts: read `skills/portfolio-usage-report/SKILL.md` first.

## Common Date Windows
- Last 30 days: today minus 30 days → today
- Last 90 days: today minus 90 days → today
- Last 6 months: today minus 180 days → today
- Last 12 months: today minus 365 days → today

## Regressions
- [YYYY-MM-DD] Always update skill file when a new event name is verified working.
