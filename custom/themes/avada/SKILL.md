---
name: theme-avada-config
description: "Use when configuring the Avada WordPress theme (ThemeFusion). Provides all available options (colors, typography, header, footer, layout, blog, WooCommerce, responsive) and procedures to apply them via MCP Content Manager abilities. Classic theme — options stored in wp_options as fusion_options."
compatibility: "Avada 7.14+. Requires WordPress 4.9+ and PHP 5.6+. Classic theme (NOT FSE)."
---

# Avada Theme Configuration

## Theme Type

**Classic theme (NOT Full Site Editing)**. All configuration is stored in `wp_options` table as a serialized array under option name `fusion_options`. Does NOT use Global Styles or theme.json.

## When to use

- The user wants to change colors, fonts, header, footer, or layout of Avada
- The user wants to configure blog, portfolio, or WooCommerce settings
- The user wants to adjust responsive breakpoints
- The user wants to set up logo, favicons, and branding
- The user wants to set up the site identity

## Inputs required

- What aspect to configure (colors, typography, header, footer, layout, blog, WooCommerce, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## Procedure

### 0) Verify the active theme

Call `mcm/theme-config-guide` — it auto-detects the active theme and confirms it is `Avada` (classic theme).

### 1) Read current configuration

```json
// Read ALL Avada options (auto-detects fusion_options)
mcm/get-theme-options {}

// Read specific options only
mcm/get-theme-options {"keys": ["primary_color", "header_layout", "layout", "site_width", "footer_widgets"]}
```

### 2) Update a single option

```json
mcm/set-theme-options {"values": {"primary_color": "#E94560"}}
```

### 3) Update multiple options at once

```json
mcm/set-theme-options {
  "values": {
    "primary_color": "#E94560",
    "header_layout": "v1",
    "layout": "wide",
    "site_width": "1200px",
    "footer_widgets": "1",
    "footer_widgets_columns": "4"
  }
}
// Dynamic CSS cache is automatically cleared after the update
```

### 4) Configure page-level options (post meta)

Avada supports per-page option overrides stored as post meta. Use `mcm/update-content` to set post meta values:

```json
// Set page-specific options
mcm/update-content {
  "id": <post_id>,
  "meta": {
    "pyre_header_bg_color": "#FF0000",
    "pyre_slider_type": "no"
  }
}
```

### 5) Configure logo and branding

After uploading images with `mcm/upload-media`, update logo options:

```json
mcm/set-theme-options {
  "values": {
    "logo": {"url": "https://example.com/wp-content/uploads/logo.png"},
    "logo_retina": {"url": "https://example.com/wp-content/uploads/logo@2x.png"},
    "mobile_logo": {"url": "https://example.com/wp-content/uploads/logo-mobile.png"},
    "fav_icon": {"url": "https://example.com/wp-content/uploads/favicon.png"}
  }
}
```

### 6) Set up site identity

```json
mcm/set-option {"name": "blogname", "value": "Site Name"}
mcm/set-option {"name": "blogdescription", "value": "Site Tagline"}
mcm/set-option {"name": "site_icon", "value": <attachment_id>}
mcm/set-option {"name": "show_on_front", "value": "page"}
mcm/set-option {"name": "page_on_front", "value": <page_id>}
mcm/set-option {"name": "page_for_posts", "value": <page_id>}
```

### 7) Clear caches after changes

The `mcm/set-theme-options` ability automatically clears Avada's dynamic CSS cache after updating. No manual cache clearing is needed.

## Important: Avada Color System

Avada 7.x+ uses a **Global Color Palette** (AWB Colors). Individual color options reference palette variables like `var(--awb-color1)` through `var(--awb-color8)`. To read the global palette:

```json
mcm/get-theme-options {"keys": ["color_palette"]}
```

## Verification

- [ ] Colors display correctly on the frontend
- [ ] Header layout and styling are correct
- [ ] Footer widgets and content display correctly
- [ ] Logo loads properly (standard, retina, mobile)
- [ ] Blog layout and meta display settings work
- [ ] WooCommerce shop page and product display are correct (if applicable)
- [ ] Responsive breakpoints trigger correctly
- [ ] Dynamic CSS has been regenerated

## Failure modes / debugging

- **Changes not visible:** The MCP ability auto-clears Avada's compiled CSS cache; clear browser cache if needed
- **Option not saving:** The `mcm/set-theme-options` ability automatically reads the full array and merges only the specified keys — it never replaces the entire array
- **Page-level override not working:** Page meta keys use `pyre_` prefix (e.g., `pyre_header_bg_color`)
- **Multilingual sites:** Option key may be language-suffixed (e.g., `fusion_options_es`)
- **Color variables:** Avada 7.x uses `var(--awb-colorN)` references — set actual hex values or update the global palette

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all option IDs with types and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared reference (see Section 0 for Classic vs FSE differences)
