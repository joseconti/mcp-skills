# Custom Skills

This directory contains custom skills that are **not** synced from the upstream [WordPress/agent-skills](https://github.com/WordPress/agent-skills) repository.

## Active skills

- **woocommerce/** — WooCommerce development patterns, hooks, HPOS, and best practices
- **site-creation/** — Complete guide for creating a WordPress site from scratch
- **themes/** — Theme configuration skills (see [themes/INDEX.md](themes/INDEX.md)):
  - **themes/wordpress-theme-customizer/** — General-purpose theme customizer (orchestrator for any theme — auto-detects type, checks for specific skill, offers standard or full scan)
  - **themes/avada/** — Avada configuration (classic theme — fusion_options: colors, header, footer, layout, blog, WooCommerce) — via `mcm/get-theme-options` / `mcm/set-theme-options`
  - **themes/dt-the7/** — The7 configuration (classic theme — the7: colors, header, footer, layout, blog, portfolio, buttons) — via `mcm/get-theme-options` / `mcm/set-theme-options`
  - **themes/twentytwentyfive/** — Twenty Twenty-Five configuration (block/FSE — Global Styles: colors, fonts, layout, templates) — via `mcm/get-global-styles` / `mcm/set-global-styles`
  - **themes/twentytwentyfour/** — Twenty Twenty-Four configuration (block/FSE — Global Styles: colors, fonts, duotones, gradients, templates) — via `mcm/get-global-styles` / `mcm/set-global-styles`
  - **themes/twentytwentythree/** — Twenty Twenty-Three configuration (block/FSE — Global Styles: colors, fonts, style variations, templates) — via `mcm/get-global-styles` / `mcm/set-global-styles`

All theme configurations are done through **MCP Content Manager abilities** (no WP-CLI required).

## Planned skills

- **wordpress-security/** — WordPress security guidelines, OWASP patterns, and hardening
- **wordpress-general/** — General WordPress coding guidelines and conventions

## Structure

Each custom skill follows the same format as official WordPress skills:

```
custom/skill-name/
├── SKILL.md           # Main instruction file
└── references/        # Detailed reference docs
    ├── topic-1.md
    └── topic-2.md
```
