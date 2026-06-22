# Pod Plugin

Pod is a sales workflow plugin powered by Pod MCP. It helps Claude Code and Codex use Pod's read-only intelligence surface for deal review, call prep, meeting debriefs, pipeline triage, stakeholder analysis, and account relationship summaries.

## Why Pod

Pod brings sales context into the agent: CRM records, Deal Coach recommendations, Prioritize signals, playbook coverage, transcripts, stakeholder sentiment, team structure, and Pod Agent synthesis. The plugin packages that context as reusable skills and Claude Code slash commands so sellers and managers get evidence-backed answers instead of generic sales advice.

This plugin package contains Pod workflow skills, Claude Code slash commands, and Pod MCP configuration. The MCP tools are served by Pod at `https://gateway.workwithpod.com/mcp`.

## Getting Started

Pod MCP requires a Pod API key. Create or request one from the API key or MCP settings in your Pod workspace, then set it before launching Claude Code or Codex:

```bash
export POD_MCP_API_KEY="your-pod-api-key"
```

### Claude Code

Install from the Claude community marketplace once the plugin is approved:

```text
/plugin marketplace add anthropics/claude-plugins-community
/plugin install pod@claude-community
```

For local testing from the repository root:

```bash
npm run setup:claude
```

This runs:

```bash
claude --plugin-dir ./pod
```

Inside Claude Code, run `/reload-plugins`, then try `/pod:deal-risk-review Acme renewal`. For local MCP testing, you can also copy the repository-level `.claude/settings.local.example.json` to `.claude/settings.local.json`, set the key there, and keep `enabledMcpjsonServers` set to `["pod"]`.

### Codex

Codex uses `pod/.codex-plugin/plugin.json` and invokes skills with `$skill-name`, not Claude Code slash commands. For local testing, register the repository root as a Codex marketplace, then install `pod`:

```bash
npm run setup:codex
```

This runs `codex plugin marketplace add "$PWD"` followed by `codex plugin add pod@pod-plugins`.

Restart Codex after changing plugin or marketplace files. Run `/mcp` and verify the bundled `pod` MCP server is enabled. If it is missing while testing, add it manually:

```bash
codex mcp add pod --url https://gateway.workwithpod.com/mcp --bearer-token-env-var POD_MCP_API_KEY
```

## Commands

Claude Code exposes the plugin workflows as `/pod:*` slash commands. Codex uses the same underlying skills with `$skill-name`.

| Claude Code command | Codex skill | Use it for | Example |
| --- | --- | --- | --- |
| `/pod:deal-risk-review` | `$deal-risk-review` | Diagnose close risk, forecast risk, stalled deals, stakeholder coverage, and missing evidence. | `/pod:deal-risk-review Globex expansion. Focus on close date and economic buyer risk.` |
| `/pod:call-summary` | `$call-summary` | Summarize calls, debrief meetings, extract commitments, open questions, tone, and follow-up actions. | `/pod:call-summary Summarize the most recent procurement call for Acme.` |
| `/pod:call-prep` | `$call-prep` | Prepare for discovery, demo, executive, renewal, procurement, legal, security, or multi-stakeholder meetings. | `/pod:call-prep Prepare me for tomorrow's security review with Northstar.` |
| `/pod:pipeline-triage` | `$pipeline-triage` | Rank focus deals, identify urgent seller actions, and separate today, next-week, and monitor work. | `/pod:pipeline-triage What should I focus on today across my open deals?` |

The plugin also includes skills that Claude Code or Codex can select automatically from natural language.

| Skill | Use it for | Example prompt |
| --- | --- | --- |
| `stakeholder-gap-analysis` | Buying committee coverage, champion strength, economic buyer engagement, missing roles, and multi-threading risk. | `Which stakeholders are missing from the Acme deal?` |
| `account-relationship-summary` | Account relationship health, engaged contacts, sentiment movement, coverage gaps, and relationship-building actions. | `Give me an account relationship summary for Northstar.` |
| `use-pod-mcp-well` | Evidence discipline, tool selection, and read-only boundary handling for any Pod workflow. | `Use Pod to review this renewal and cite the evidence you used.` |

## MCP Capabilities

Pod MCP is read-only. It retrieves curated Pod evidence and can synthesize it, but it cannot update CRM, send email, create calendar events, complete recommendations, or save Pod workflows.

| Capability | Pod MCP tools | Helps with |
| --- | --- | --- |
| CRM context | `get_crm_record_context` | Deal, account, contact, or lead context for risk review, call prep, and relationship summaries. |
| Deal Coach recommendations | `get_deal_recommendations` | Flags, recommended seller actions, missing stakeholders, stale follow-up, and deal health concerns. |
| Pipeline priorities | `get_deal_priorities` | Prioritize scores, ranking signals, temperature, pace, urgency, and focus deal selection. |
| Playbook and framework coverage | `get_deal_framework_coverage`, `search_workspace_playbooks` | MEDDPICC, BANT, NEAT, ALIGN, custom methodology gaps, and workspace-specific playbook language. |
| Call and transcript evidence | `get_transcript_call_ids`, `get_transcripts`, `get_transcript_summaries`, `search_transcript_chunks` | Call summaries, objections, commitments, stakeholder mentions, decision process, pricing, security, legal, and next steps. |
| Stakeholder sentiment | `get_contact_sentiment` | Champion health, economic buyer engagement, sentiment changes, relationship risk, and follow-up needs. |
| Team context | `get_team_structure` | Manager or team-level views for pipeline triage and coaching. |
| Broad synthesis | `ask_pod_agent`, `get_ask_pod_agent_run` | Ambiguous record matching, cross-account research, multi-source synthesis, and "what should I focus on" questions. |

## How It Works

Every component is file-based: Markdown skills and commands plus JSON manifests. There is no build step.

```text
pod/
├── .claude-plugin/plugin.json   # Claude Code manifest
├── .codex-plugin/plugin.json    # Codex manifest
├── .mcp.json                    # Pod MCP connection
├── commands/                    # Claude Code slash commands
└── skills/                      # Shared domain workflows
```

Skills encode Pod workflow guidance and are selected automatically when relevant. Commands are explicit Claude Code entry points. The MCP config wires Claude Code to Pod's hosted read-only MCP server. Codex uses `pod/.codex-plugin/plugin.json`, which points at `skills/` and `.mcp.json` relative to the `pod/` folder.

## Read-Only Boundary

Pod MCP v1 is read-only. The plugin can retrieve and synthesize evidence, draft suggested language, and recommend seller actions. It must not claim to update CRM fields, send emails, create calendar events, complete Deal Coach recommendations, or save Pod Skills or automations.

When a write action is needed, the assistant should explain the boundary and tell the user what to do in Pod, CRM, email, or calendar.

## Validation

Run:

```bash
npm run setup:claude
npm run setup:codex
npm run validate:claude
npm run validate:codex
```

Suggested smoke tests:

- From the repository root, load locally with `claude --plugin-dir ./pod`.
- Run `/pod:deal-risk-review` or `$deal-risk-review` with Pod MCP connected.
- Run a Pod prompt without MCP connected and verify the assistant asks for setup instead of inventing Pod data.
- Review outputs for evidence citations and read-only boundary compliance.

## Troubleshooting

- `POD_MCP_API_KEY` is not set: export the environment variable before launching Claude Code or Codex. For Claude Code local testing, you can also set it in `.claude/settings.local.json`.
- Pod MCP tools are missing: verify the MCP server is connected and restart Claude Code or Codex, or run `/reload-plugins` in Claude Code.
- No deal or call evidence is found: provide a more specific deal name, account name, CRM record ID, call ID, participant, or date range.
- Your workspace uses a custom Gateway host: replace the `.mcp.json` URL with the host provided by Pod.

## Repository Notes

The root [README.md](../README.md) describes the plugin marketplace wrapper. Marketplace submission notes live in [SUBMISSION.md](../SUBMISSION.md).
