---
description: Prepare discovery, demo, executive, renewal, or multi-stakeholder meetings using Pod MCP evidence. Use when the user asks for call prep, meeting prep, discovery prep, demo prep, executive prep, objection prep, or a conversation plan.
---

# Call Prep

Use this skill to prepare a seller for an upcoming or requested customer meeting. Meeting prep should combine known facts, gaps, stakeholder context, playbook coverage, likely objections, and a concrete conversation plan.

## Evidence To Gather

Use:

- `get_crm_record_context` for the deal, account, contact, or lead.
- `get_deal_recommendations` for Deal Coach flags that should shape the meeting.
- `get_deal_framework_coverage` and `search_workspace_playbooks` for methodology gaps and topics to cover.
- `get_transcript_call_ids`, `get_transcript_summaries`, and `search_transcript_chunks` for recent conversation history.
- `get_contact_sentiment` for attendees and known stakeholders.
- `get_deal_priorities` when the prep should account for deal urgency or risk.

Use `ask_pod_agent` for broad prep when the user gives only an account name, asks for "everything I need to know", or needs synthesis across recent activity, recommendations, stakeholders, and playbooks.

## Meeting Types

Adapt the plan to the meeting:

- Discovery: uncover pain, urgency, decision process, success metrics, budget, and current state.
- Demo: tie product moments to known pain, buying criteria, and stakeholder priorities.
- Executive: focus on business impact, risk, strategic value, and decision path.
- Multi-stakeholder: tailor messages by role and expose coverage gaps.
- Procurement/legal/security: clarify paper process, owners, timeline, blockers, and evidence needed.

## Output Format

Return:

1. `Objective`: the recommended meeting goal.
2. `Known Facts`: what Pod evidence says about the deal/account and attendees.
3. `Gaps To Close`: missing qualification, stakeholder, framework, or process evidence.
4. `Likely Objections`: objections or risks to prepare for, tied to evidence when possible.
5. `Stakeholder Angles`: role-by-role talk tracks and concerns.
6. `Conversation Plan`: agenda, key questions, and recommended closing ask.
7. `Evidence Used`: Pod tools and identifiers used.

Respect the read-only boundary. You may draft suggested language, but do not claim Pod MCP sent emails, updated CRM, or created calendar events.
