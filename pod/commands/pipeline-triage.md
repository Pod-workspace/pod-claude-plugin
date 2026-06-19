---
description: Rank pipeline focus deals and actions using Pod MCP priorities, recommendations, and evidence.
argument-hint: "[owner, team, time horizon, deal list, or focus]"
---

# Pod Pipeline Triage

Run the Pod Pipeline Triage workflow for:

`$ARGUMENTS`

Use the `use-pod-mcp-well` and `pipeline-triage` skills. Prefer `get_deal_priorities` and `get_deal_recommendations` for ranking evidence, then add framework coverage, transcripts, sentiment, and `ask_pod_agent` synthesis when useful.

Return:

1. Focus order.
2. Today.
3. Next 7 Days.
4. Monitor.
5. Evidence used.
6. Missing evidence.

Keep recommendations read-only and seller-actionable. Do not claim to complete Deal Coach recommendations or update Pod/CRM records.
