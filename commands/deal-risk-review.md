---
description: Review a deal for risk using Pod MCP evidence.
argument-hint: "<deal name, account name, or CRM record id> [specific concern]"
---

# Pod Deal Risk Review

Run the Pod Deal Risk Review workflow for:

`$ARGUMENTS`

Use the `use-pod-mcp-well` and `deal-risk-review` skills. Gather direct Pod MCP evidence first when possible, then use `ask_pod_agent` for broad synthesis or ambiguous record matching.

Return a practical seller-ready review with:

1. Verdict.
2. Evidence.
3. Ranked risks.
4. Missing evidence.
5. Recommended next actions.

Respect Pod MCP v1's read-only boundary. Do not claim to update CRM, send email, create calendar events, complete recommendations, or save Pod Skills.
