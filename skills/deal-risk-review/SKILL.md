---
name: deal-risk-review
description: Review deal risk using Pod MCP evidence. Use when the user asks for deal health, risk assessment, stalled deal diagnosis, close date reality checks, forecast risk, or why a deal may be at risk.
---

# Deal Risk Review

Use this skill to diagnose deal health and risk from Pod evidence. Adapt Pod Deal Coach patterns: deal activity, stakeholder coverage, velocity, days since last stage, touchpoint density, close date realism, contact roles, framework gaps, and stakeholder sentiment.

## Evidence To Gather

Start with direct Pod MCP reads when identifiers are available:

- `get_crm_record_context` for the deal and account context.
- `get_deal_recommendations` for Deal Coach flags and recommendations.
- `get_deal_priorities` for priority, temperature, pace, and risk signals.
- `get_deal_framework_coverage` for MEDDPICC, BANT, NEAT, ALIGN, or custom playbook gaps.
- `get_transcript_call_ids`, `get_transcript_summaries`, and `search_transcript_chunks` for recent call evidence.
- `get_contact_sentiment` for champion, economic buyer, evaluator, procurement, legal, security, and other key contacts when contact emails are known.

Use `ask_pod_agent` when record matching is ambiguous, the user asks for an overall synthesis, or you need broad context across CRM, transcript, email, calendar, recommendations, priorities, and playbooks.

## Review Dimensions

Check:

- Activity: quiet periods, stale follow-up, or missing next meetings.
- Velocity: slow stage movement or stalled stage age.
- Close date: whether timing is supported by agreement path, procurement, legal, security, and executive approval evidence.
- Stakeholders: buying committee depth, champion strength, economic buyer engagement, multi-threading, missing roles, and sentiment.
- Playbook coverage: qualification gaps, decision criteria, decision process, paper process, budget, authority, need, timeline, or workspace-specific framework topics.
- Commitments: mutual action plan, next steps, buyer-owned actions, and evidence of urgency.

## Output Format

Return:

1. `Verdict`: On track, Watch, or At risk, with one sentence explaining why.
2. `Evidence`: the strongest Pod signals, each tied to the tool or evidence family used.
3. `Risks`: ranked risk list with severity and impact.
4. `Missing Evidence`: important fields or signals that were unavailable.
5. `Recommended Next Actions`: seller actions, written as recommendations only.

Respect Pod MCP's read-only boundary. Do not say you updated CRM, sent email, created meetings, completed recommendations, or saved a Pod Skill.
