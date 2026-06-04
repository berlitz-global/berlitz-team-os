# Customer Insights

Customer feedback, account context, and call notes for named accounts.

## Segments

| Segment | Description |
|---------|-------------|
| Enterprise | Managed accounts with complex needs (SSO, compliance, dedicated support) |
| Growth | Mid-market accounts with expansion potential |
| Self-serve | Long-tail, no individual account management |

Only named/managed accounts get folders. Self-serve customers are tracked through aggregate analytics.

## Named Accounts

| Account | Segment | Folder |
|---------|---------|--------|
| | | |

## Finding Customer Data

| Looking for... | Where to find it |
|----------------|-----------------|
| Account context, goals, risks | `accounts/{customer}/account-context.md` |
| Call summaries | `accounts/{customer}/calls/summaries/` |
| Call transcripts | `accounts/{customer}/calls/transcripts/` |
| Feature requests for a customer | Linear / Jira / Asana: filter by customer label |
| Escalations | Linear / Jira / Asana: filter by `type:escalation` + customer label |

## Processing Customer Calls

When processing a new customer call:
1. Save summary to `accounts/{customer}/calls/summaries/{date}.md`
2. Save transcript to `accounts/{customer}/calls/transcripts/{date}.md`
3. Update `accounts/{customer}/account-context.md` with new insights
4. Log feature requests in Linear / Jira / Asana with the customer label
