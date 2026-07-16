# Pod Plugins

Pod plugins bring Pod's sales intelligence into Claude Code and Codex. They package Pod workflow skills, Claude Code slash commands, and Pod MCP configuration so sellers and managers can review deals, prep for meetings, debrief calls, triage pipeline, and understand stakeholder relationships from Pod evidence.

## Plugin Marketplace

This repository is a plugin marketplace with one plugin today:

| Plugin           | How it helps                                                                                                                  | Connector |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------- | --------- |
| **[pod](./pod)** | Review deal risk, prep calls, summarize meetings, triage pipeline, analyze stakeholders, and summarize account relationships. | Pod MCP   |

The plugin does not implement Pod MCP tools. It points Claude Code and Codex at Pod's hosted read-only MCP server: `https://gateway.workwithpod.com/mcp`.

## Getting Started

Pod MCP requires a Pod API key. Create or request one from [Pod API settings](https://app.workwithpod.com/dashboard/account-settings/api), then set it before launching Claude Code or Codex:

```bash
export POD_MCP_API_KEY="your-pod-api-key"
```

### Claude Code

Install from the Claude community marketplace once the plugin is approved:

```text
/plugin marketplace add anthropics/claude-plugins-community
/plugin install pod@claude-community
```

For local testing from this repository:

```bash
npm run test:claude
```

This runs:

```bash
claude --plugin-dir ./pod
```

To install the local plugin into Claude Code for this repository:

```bash
npm run setup:claude:local
```

This adds the current repository as a local Claude marketplace and installs `pod@pod-plugins` with local scope.

Once installed, skills fire when relevant and slash commands are available in your session, such as `/pod:deal-risk-review` and `/pod:call-prep`.

### Codex

Codex uses `pod/.codex-plugin/plugin.json` and the plugin files under `pod/`. For local testing, set up the repository root as a Codex marketplace, then install `pod`:

```bash
npm run setup:codex:local
```

This runs `codex plugin marketplace add "$PWD"` followed by `codex plugin add pod@pod-plugins`.

Codex invokes the same workflows as skills, such as `$deal-risk-review`, `$call-summary`, `$call-prep`, and `$pipeline-triage`.

## How Plugins Work

This repository follows the same shape as a marketplace collection: repository-level marketplace metadata points to plugin folders, and each plugin folder contains its own Claude Code manifest, commands, skills, and MCP configuration.

```text
pod-plugins/
├── .claude-plugin/marketplace.json  # Claude Code marketplace listing
├── .agents/plugins/marketplace.json # Codex local marketplace listing
├── pod/
│   ├── .claude-plugin/plugin.json   # Pod Claude Code manifest
│   ├── .codex-plugin/plugin.json    # Pod Codex manifest
│   ├── .mcp.json                    # Pod MCP connection
│   ├── commands/                    # Claude Code slash commands
│   └── skills/                      # Shared Pod workflow skills
```

- **Skills** encode Pod workflow expertise and are selected automatically when relevant.
- **Commands** are explicit Claude Code workflows, namespaced as `/pod:*`.
- **MCP configuration** connects the plugin to Pod's read-only intelligence surface.

Every component is file-based: Markdown and JSON, with no build step.

## Pod Plugin

See [pod/README.md](./pod/README.md) for command tables, MCP capabilities, usage examples, troubleshooting, and the read-only boundary.

## Development

Run both validators before release or submission:

```bash
npm run validate:claude
npm run validate:codex
```
