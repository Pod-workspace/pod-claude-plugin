---
name: account-relationship-summary
description: Summarize account-level relationship health, engaged contacts, sentiment, coverage gaps, and relationship-building actions using Pod MCP. Use when the user asks for an account relationship summary, account health, relationship map, contact coverage, or account-level stakeholder readout.
---

# Account Relationship Summary

Use this skill to summarize account-level relationship health from Pod evidence. The goal is to help a seller or manager understand who is engaged, where sentiment is moving, what coverage gaps exist, and what relationship-building actions matter next.

## Evidence To Gather

Use:

- `get_crm_record_context` for account, contact, lead, and related deal context.
- `get_contact_sentiment` for engaged contacts and known stakeholders.
- `get_transcript_call_ids`, `get_transcript_summaries`, and `search_transcript_chunks` for recent account conversations.
- `get_deal_recommendations` and `get_deal_priorities` for open deal risks tied to the account.
- `get_deal_framework_coverage` for playbook or process gaps that affect relationship health.

Use `ask_pod_agent` for broad account synthesis, especially when the user asks for "relationship health", "who matters at this account", or cross-deal/account history.

## Relationship Dimensions

Check:

- Engagement breadth: active contacts, inactive contacts, single-threaded risk, and multi-threading strength.
- Role coverage: champion, economic buyer, decision maker, procurement, legal, security, IT, implementation, and end users.
- Sentiment: positive, negative, neutral, trending up/down, and unknown.
- Recent activity: calls, emails, meetings, commitments, open questions, and follow-up needs.
- Account risks: stalled momentum, missing next step, unclear decision process, stakeholder churn, or unresolved objections.

## Output Format

Return:

1. `Relationship Health`: strong, mixed, weak, or unknown, with a short rationale.
2. `Engaged Contacts`: key people, roles, sentiment, and recent evidence.
3. `Coverage Gaps`: missing roles or relationships to build.
4. `Recent Signals`: important calls, commitments, objections, or sentiment changes.
5. `Recommended Relationship Moves`: practical next actions for the seller.
6. `Evidence Used`: tools, record IDs, call IDs, dates, and other identifiers where available.

Respect the read-only boundary. Recommend actions; do not claim to update CRM, send emails, create meetings, or save Pod workflows.
