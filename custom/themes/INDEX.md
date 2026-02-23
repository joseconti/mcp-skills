# Theme Configuration Skills Index

This directory contains skills for AI-driven configuration of WordPress themes. Each skill documents all configurable options for a specific theme and provides procedures to apply settings via MCP Content Manager abilities.

## General Theme Customizer

For themes **without** a specific skill listed below, use the **[wordpress-theme-customizer](wordpress-theme-customizer/)** skill. It acts as an orchestrator that:

1. Auto-detects the active theme and its type (classic or block/FSE)
2. Checks if a theme-specific skill exists
3. If not, offers a standard scan or a full source code scan to discover all configuration options
4. Executes changes and optionally generates a new theme-specific skill

**Always start here** if you are unsure which skill to use.

## Available Themes

| Theme | Directory | Slug | Type | Min WordPress | Options | Coverage |
|-------|-----------|------|------|---------------|---------|----------|
| Avada | [avada/](avada/) | `Avada` | Classic | 4.9+ | 600+ | 100% — 33 sections, 5-phase guided setup |
| The7 | [dt-the7/](dt-the7/) | `dt-the7` | Classic | 6.6+ | 350+ | 100% — All options incl. mobile header, micro-widgets, floating header, stripes, social buttons, advanced |
| Twenty Twenty-Five | [twentytwentyfive/](twentytwentyfive/) | `twentytwentyfive` | Block (FSE) | 6.7+ | 200+ | 100% — 8 style variations, 98 patterns, 30+ per-block styles, 7 extra fonts |
| Twenty Twenty-Four | [twentytwentyfour/](twentytwentyfour/) | `twentytwentyfour` | Block (FSE) | 6.4+ | 180+ | 100% — 7 style variations, 57 patterns, 29 per-block styles, 5 custom block styles |
| Twenty Twenty-Three | [twentytwentythree/](twentytwentythree/) | `twentytwentythree` | Block (FSE) | 6.1+ | 120+ | 100% — 10 style variations, 7 patterns, 21 per-block styles, 5 font families |

## CRITICAL: Classic vs Block Theme Differences

**You MUST identify the theme type before attempting configuration.** The storage mechanism is completely different.

### How to detect the theme type

Use `mcm/theme-config-guide` — it auto-detects the active theme and tells you whether it is a block theme or classic theme.

### Block Themes (TT3, TT4, TT5)

Configuration stored in **Global Styles** (`wp_global_styles` post type as JSON):
- Colors, typography, spacing, layout, per-block styles
- Managed via **`mcm/get-global-styles`** and **`mcm/set-global-styles`** MCP abilities

### Classic Themes (Avada, The7)

Configuration stored in **wp_options** as serialized arrays:
- **Avada**: option name `fusion_options`
- **The7**: option name `the7mk2`
- Managed via **`mcm/get-theme-options`** and **`mcm/set-theme-options`** MCP abilities

See [global-styles-api.md](global-styles-api.md) Section 0 for the full comparison.

## MCP Abilities for Theme Configuration

| Ability | Purpose | Theme Type |
|---------|---------|------------|
| `mcm/theme-config-guide` | Get the configuration guide for the active theme | All |
| `mcm/get-global-styles` | Read Global Styles (colors, fonts, layout, spacing) | Block (FSE) |
| `mcm/set-global-styles` | Write/merge Global Styles | Block (FSE) |
| `mcm/reset-global-styles` | Reset Global Styles to theme defaults | Block (FSE) |
| `mcm/get-theme-options` | Read classic theme options | Classic |
| `mcm/set-theme-options` | Update classic theme options (partial merge) | Classic |
| `mcm/get-theme-mod` | Read theme modifications (custom_logo, colors) | All |
| `mcm/set-theme-mod` | Set theme modifications | All |
| `mcm/set-option` | Set site options (blogname, show_on_front, etc.) | All |

## Shared Reference

- **[global-styles-api.md](global-styles-api.md)** — API reference for theme configuration via MCP abilities, and Classic vs FSE comparison.

## Usage

1. Call `mcm/theme-config-guide` to auto-detect the active theme and get the full configuration guide
2. Read the theme's reference data (returned by the guide) for exact option IDs, values, and defaults
3. Use the appropriate MCP abilities to read current values and apply changes
4. ALWAYS ask the user what they want to change before applying any configuration
