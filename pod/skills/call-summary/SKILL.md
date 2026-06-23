---
name: call-summary
description: Summarize sales calls and meeting debriefs using Pod MCP transcripts and summaries. Use when the user asks for a call summary, meeting debrief, recent call recap, commitments, open questions, sentiment shifts, or post-meeting next steps.
---

# Call Summary / Meeting Debrief

Use this skill to produce a practical post-meeting debrief from Pod transcript evidence. Pod Meeting Briefs use structured summaries with purpose, key takeaways, topics discussed, and next steps; keep the answer useful for seller follow-up and deal review.

## Evidence To Gather

Use:

- `get_transcript_call_ids` to find relevant calls by deal, account, participant, or date range.
- `get_transcript_summaries` for concise summaries when call IDs are known.
- `get_transcripts` when details or speaker-level evidence is needed.
- `search_transcript_chunks` for specific topics such as pricing, security, procurement, legal, implementation, objections, competitors, urgency, success metrics, next steps, or stakeholder names.
- `get_crm_record_context`, `get_deal_recommendations`, and `get_deal_framework_coverage` when the user wants the call interpreted in deal context.
- `get_contact_sentiment` when the user asks about tone or relationship movement.

Use `ask_pod_agent` for multi-call debriefs, ambiguous call matching, or when the user asks for a synthesis across calls and CRM context.

## Output Format

Return:

1. `Summary`: 3-5 sentences on what happened and why it matters.
2. `Key Takeaways`: customer needs, priorities, objections, timeline, process, and decision criteria.
3. `Commitments`: seller commitments and buyer commitments, separated when possible.
4. `Open Questions`: unresolved issues or missing evidence.
5. `Sentiment / Tone`: any concrete sentiment shift or stakeholder signal from Pod evidence.
6. `Next Steps`: recommended follow-up actions and suggested owner when clear.
7. `Evidence Used`: call IDs, summaries, transcript chunks, or Pod tools used.

If no transcript evidence is connected, say so and ask the user to connect Pod MCP or provide the call context. Do not hallucinate call content.
