---
description: Summarize a recent sales call or meeting using Pod MCP transcripts and context.
argument-hint: "<deal/account/call id/date range> [focus topics]"
---

# Pod Call Summary

Run the Pod Call Summary / Meeting Debrief workflow for:

`$ARGUMENTS`

Use the `use-pod-mcp-well` and `call-summary` skills. Find relevant call IDs, transcript summaries, transcript chunks, and deal/account context. Use `ask_pod_agent` when matching the call or synthesizing multiple calls is ambiguous.

Return:

1. Summary.
2. Key takeaways.
3. Commitments.
4. Open questions.
5. Sentiment or tone.
6. Next steps.
7. Evidence used.

If Pod MCP or transcript evidence is unavailable, ask for connection/context instead of inventing call content.
