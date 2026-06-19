---
description: Analyze buying committee coverage, champion health, economic buyer engagement, contact sentiment, and multi-threading gaps using Pod MCP. Use when the user asks about stakeholder gaps, buying committee risk, champion strength, economic buyer coverage, missing roles, or multi-threading.
---

# Stakeholder Gap Analysis

Use this skill to analyze whether a deal has the right people engaged. Adapt Pod Stakeholder Mapping and Contact Health Card patterns: buying committee coverage, recommended roles, win-rate context, contact assignment, contact sentiment, concerns, excitement signals, follow-up needs, questions, challenges, and objectives.

## Evidence To Gather

Use:

- `get_crm_record_context` for current contacts, roles, account/deal context, and known stakeholders.
- `get_deal_recommendations` for stakeholder-related recommendations such as `flag_stakeholders`, `flag_contact_roles`, `missing_stakeholder`, `stakeholder_sentiment`, and `stakeholder_follow_up`.
- `get_contact_sentiment` for known contacts and likely stakeholders.
- `get_deal_framework_coverage` for methodology topics tied to authority, champion, decision process, budget, or paper process.
- `get_transcript_summaries` and `search_transcript_chunks` for evidence of influence, objections, introductions, decision criteria, or approval process.

Use `ask_pod_agent` when the user asks for a broad relationship or buying committee read, or when stakeholder names and roles need to be synthesized across multiple sources.

## Analysis Dimensions

Check:

- Champion: who is advocating, what commitments they made, and whether they introduced others.
- Economic buyer: whether the budget owner or executive decision maker is engaged.
- Decision process: procurement, legal, security, IT, implementation, and executive approval owners.
- Multi-threading: number and quality of active relationships versus single-threaded risk.
- Sentiment: negative, positive, declining, improving, or unknown relationship signals.
- Missing roles: roles absent from the buying committee or not yet mapped.

## Output Format

Return:

1. `Coverage Verdict`: strong, partial, or weak buying committee coverage.
2. `Known Stakeholders`: names, roles, sentiment, and evidence where available.
3. `Gaps`: missing or under-engaged roles and why they matter.
4. `Risks`: single-threading, weak champion, absent economic buyer, negative sentiment, or stalled follow-up.
5. `Recommended Actions`: suggested introductions, questions, and follow-up paths.
6. `Evidence Used`: Pod tools and concrete evidence identifiers.

Do not say a stakeholder does not exist just because evidence is missing. Say the stakeholder was not found in the available Pod evidence.
