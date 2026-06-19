---
name: pipeline-triage
description: Rank and triage pipeline focus using Pod MCP deal priorities, recommendations, framework coverage, transcript evidence, and Pod Agent synthesis. Use when the user asks what deals to focus on, pipeline triage, top deals, at-risk deals, watchlist review, or manager pipeline review.
---

# Pipeline Triage

Use this skill to help an AE or sales manager decide where to spend time. Adapt Pod Prioritize and Pipeline Coach patterns: ranked focus deals, Today / Next 7 Days actions, risk signals, urgency, temperature, pace, recommendation buckets, and evidence-backed next steps.

## Evidence To Gather

Use:

- `get_deal_priorities` for priority score, temperature, pace, risk, and ranking signals.
- `get_deal_recommendations` for Deal Coach flags and recommendations across focus deals.
- `get_deal_framework_coverage` for methodology gaps on high-priority or at-risk deals.
- `get_crm_record_context` for deal/account details when explaining a rank.
- `get_transcript_summaries` and `search_transcript_chunks` when transcript evidence explains urgency, objections, or next steps.
- `get_contact_sentiment` for stakeholder risk when contacts are known.

Use `ask_pod_agent` for broad pipeline questions such as "what should I focus on today?" or "triage my open deals" because the best answer may require cross-deal synthesis.

## Ranking Logic

Prioritize deals with a combination of:

- High revenue or strategic value when available.
- High urgency, late-stage timing, close date pressure, or forecast exposure.
- Risk signals: stale activity, weak stakeholder coverage, slow velocity, missing roles, negative sentiment, framework gaps, or unclear next step.
- Actionability: a clear seller action can reduce risk or create momentum.
- Watchlist or manager-relevant context when provided.

## Output Format

Return:

1. `Focus Order`: ranked deals with one-line rationale.
2. `Today`: actions that should happen immediately.
3. `Next 7 Days`: important but less urgent actions.
4. `Monitor`: deals that need watching but not immediate action.
5. `Evidence Used`: priorities, recommendations, transcripts, sentiment, framework coverage, or Pod Agent synthesis.
6. `Missing Evidence`: unavailable deal context or signals that could change the rank.

Do not present recommendations as completed work. Pod MCP v1 can inform prioritization but cannot update CRM, send emails, or complete Deal Coach recommendations.
