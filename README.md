# MCP Skills — WordPress Coding Guidelines for AI

WordPress coding guidelines served to AI assistants via MCP (Model Context Protocol).

## What is this?

This repository is a controlled fork of [WordPress/agent-skills](https://github.com/WordPress/agent-skills) — the official WordPress repository containing expert-level coding knowledge for AI assistants.

It is consumed by the [MCP Content Manager for WordPress](https://plugins.joseconti.com/) plugin through the `mcm/coding-guidelines` ability, which fetches these guidelines and delivers them to any AI assistant connected via MCP.

## How it works

```
WordPress/agent-skills  (upstream, community-maintained)
        |
        |  periodic sync / selective merge
        v
joseconti/mcp-skills  (this repo — primary source, controlled)
        |
        v
MCP Content Manager plugin  (mcm/coding-guidelines tool)
        |
        v
AI Assistant (Claude, ChatGPT, Gemini, Cursor, Codex...)
```

The `mcm/coding-guidelines` tool uses a 3-level fallback:

1. **This repo** (primary) — stable, controlled URL
2. **WordPress/agent-skills** (fallback) — official upstream
3. **Offline fallback** — 10 essential rules embedded in the plugin

## Repository structure

```
mcp-skills/
├── manifest.json              # Index of all skills for the MCP tool
├── wp-plugin-development/     # Plugin architecture, hooks, security...
├── wp-block-development/      # Gutenberg blocks, block.json...
├── wp-block-themes/           # Block themes, theme.json...
├── wp-rest-api/               # REST API endpoints, auth, schema...
├── wp-performance/            # Caching, DB queries, profiling...
├── wp-wpcli-and-ops/          # WP-CLI operations, automation...
├── wp-phpstan/                # PHPStan for WordPress...
├── wp-interactivity-api/      # Interactivity API directives...
├── wp-playground/             # WordPress Playground...
├── wp-abilities-api/          # WordPress Abilities API...
├── wpds/                      # WordPress Design System
├── wordpress-router/          # Project classification / routing
├── wp-project-triage/         # Repo type detection
└── custom/                    # Custom skills (WooCommerce, security...)
```

Each skill directory contains:
- `SKILL.md` — Main instruction file (YAML frontmatter + procedural guide)
- `references/` — Detailed topic-specific documentation
- `scripts/` — Deterministic helper scripts (Node.js, not used by MCP)

## Usage

The AI assistant calls:

```
mcm/coding-guidelines(context="all")        → List all available topics
mcm/coding-guidelines(context="plugin")     → Get plugin development guidelines
mcm/coding-guidelines(context="plugin", reference="security") → Get specific reference
mcm/coding-guidelines(context="plugin", include_references=true) → Get everything
```

## License

Skills synced from WordPress/agent-skills are licensed under GPL-2.0-or-later.
Custom skills in `custom/` are also GPL-2.0-or-later.
