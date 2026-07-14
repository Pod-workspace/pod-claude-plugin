---
name: use-pod-mcp-well
description: Use Pod MCP correctly for sales workflow research. Apply this whenever a user asks an agent to use Pod, Pod MCP, deal intelligence, transcripts, recommendations, priorities, playbooks, stakeholder sentiment, or account context.
---

# Use Pod MCP Well

Use this skill whenever Pod context may be available through Pod MCP. Pod MCP is Pod's intelligence surface for sales workflows. It exposes curated Pod evidence for deal, account, call, and stakeholder research.

## Tool Selection Policy

Prefer direct Pod MCP read tools when the question asks for crisp evidence retrieval:

- `get_crm_record_context` for a known deal, account, contact, or lead.
- `get_deal_recommendations` for Deal Coach flags and recommendations.
- `get_deal_priorities` for Prioritize scores, ranking signals, and focus deals.
- `get_deal_framework_coverage` for playbook or methodology gaps.
- `get_transcript_call_ids`, `get_transcripts`, `get_transcript_summaries`, and `search_transcript_chunks` for call-level evidence.
- `search_workspace_playbooks` for methodology definitions or workspace-specific playbook language.
- `get_contact_sentiment` for relationship tone and sentiment.
- `get_team_structure` for manager or team context.

Use `ask_pod_agent` for broad research or synthesis tasks where the answer depends on multiple evidence families, ambiguous record matching, cross-account pattern finding, or "what changed / what should I focus on" style reasoning. Check its runtime description for MCP servers available internally to Pod Agent. If a needed server is not listed but is available to the external agent, query it first and pass concise findings to `ask_pod_agent` as `context`. If `ask_pod_agent` returns a `runId` and recovery instructions, use `get_ask_pod_agent_run` when needed to recover the final answer.

## Evidence Discipline

Be explicit about which Pod evidence was used. Cite tool names and concrete identifiers when available, such as deal names, record IDs, call IDs, call dates, contact emails, recommendation types, framework topics, or priority scores.

Distinguish these cases:

- Evidence found: summarize the signal and cite its source.
- Evidence missing: say the data was not available in the connected Pod evidence.
- Evidence negative: say the available evidence suggests the signal is absent.
- Tool unavailable or MCP disconnected: ask the user to connect Pod MCP or provide the relevant record context.

Do not infer facts from silence. Avoid phrases like "there is no champion" unless Pod evidence actually supports that conclusion. Prefer "I did not find champion evidence in the available Pod context."

## Default Response Shape

For Pod workflow answers, use:

1. Verdict or answer.
2. Evidence used.
3. Risks, gaps, or caveats.
4. Recommended next actions.

Keep the output practical for an account executive or sales manager. Avoid generic MCP implementation details unless the user asks.
