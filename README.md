# Pod Claude Plugin

Pod is a sales workflow plugin powered by Pod MCP. It teaches Claude how to use Pod's read-only intelligence surface for deal review, call prep, meeting debriefs, pipeline triage, stakeholder analysis, and account relationship summaries.

This repository is the source of truth for the Claude plugin package. The plugin does not implement Pod MCP tools; it packages skills, slash commands, manifests, optional MCP configuration, and submission materials.

## What Is Included

- Seven Claude plugin skills:
  - Use Pod MCP Well
  - Deal Risk Review
  - Call Summary / Meeting Debrief
  - Call Prep
  - Pipeline Triage
  - Stakeholder Gap Analysis
  - Account Relationship Summary
- Four slash command entry points:
  - `/pod:deal-risk-review`
  - `/pod:call-summary`
  - `/pod:call-prep`
  - `/pod:pipeline-triage`
- Optional `.mcp.json` configuration for Pod MCP.
- Marketplace metadata in `.claude-plugin/marketplace.json`.

## Install For Local Testing

From this repository:

```bash
claude --plugin-dir .
```

Inside Claude Code, run:

```text
/reload-plugins
```

Then try:

```text
/pod:deal-risk-review Acme renewal
/pod:call-summary last call with Acme
/pod:call-prep executive meeting for Acme
/pod:pipeline-triage my open deals this week
```

## Install From Marketplace

After the public repository is available, users can add the marketplace and install the plugin:

```text
/plugin marketplace add Pod-workspace/pod-claude-plugin
/plugin install pod@pod-plugins
```

## Connect Pod MCP

Pod MCP requires a Pod API key. Create or request a Pod MCP API key from the API key or MCP settings available to your Pod workspace. If you do not see this setting, ask your workspace admin or Pod support to enable MCP access.

Set the key in your shell before launching Claude Code:

```bash
export POD_MCP_API_KEY="your-pod-api-key"
```

This plugin includes an optional `.mcp.json` that points at:

```text
https://api.workwithpod.com/mcp
```

If your workspace uses a dedicated Pod Gateway host, copy `.mcp.json`, replace `https://gateway.workwithpod.com/mcp` with the host provided by Pod, and connect that MCP server manually in Claude Code.

Manual MCP config:

```json
{
  "mcpServers": {
    "pod-mcp": {
      "type": "http",
      "url": "https://api.workwithpod.com/mcp",
      "headers": {
        "Authorization": "Bearer ${POD_MCP_API_KEY}"
      }
    }
  }
}
```

## Example Prompts

```text
/pod:deal-risk-review Globex expansion. Focus on close date and economic buyer risk.
```

```text
/pod:call-summary Summarize the most recent procurement call for Acme.
```

```text
/pod:call-prep Prepare me for tomorrow's security review with Northstar.
```

```text
/pod:pipeline-triage What should I focus on today across my open deals?
```

Claude can also invoke the skills automatically when you ask natural-language questions such as:

```text
Which stakeholders are missing from the Acme deal?
```

```text
Give me an account relationship summary for Northstar.
```

## Read-Only Boundary

Pod MCP v1 is read-only. The plugin may help Claude retrieve and synthesize evidence, draft suggested language, and recommend next steps. It must not claim to update CRM fields, send emails, create calendar events, complete Deal Coach recommendations, or save Pod Skills or automations.

When a write action is needed, Claude should explain the boundary and tell the user what to do in Pod, CRM, email, or calendar.

## Validation

Run:

```bash
claude plugin validate .
```

If local tooling is not installed or the command is unavailable, update Claude Code and rerun the same command before submitting to a marketplace.

Suggested smoke tests:

- Load locally with `claude --plugin-dir .`.
- Run `/pod:deal-risk-review` or `/pod:call-summary` with Pod MCP connected.
- Run a command without Pod MCP connected and verify Claude asks for setup instead of hallucinating Pod data.
- Review outputs for evidence citations and read-only boundary compliance.

## Troubleshooting

- `POD_MCP_API_KEY` is not set: export the environment variable before launching Claude Code.
- Pod MCP tools are missing: verify the MCP server is connected and restart Claude Code or run `/reload-plugins`.
- No deal or call evidence is found: provide a more specific deal name, account name, CRM record ID, call ID, participant, or date range.
- Your workspace uses a custom Gateway host: replace the `.mcp.json` URL with the host provided by Pod.
