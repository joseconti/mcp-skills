---
name: theme-dt-the7-config
description: "Use when configuring The7 WordPress theme (Dream-Theme). Provides all available options (colors, typography, header, footer, layout, blog, portfolio, buttons, page titles) and procedures to apply them via MCP Content Manager abilities. Classic theme — options stored in wp_options as the7mk2."
compatibility: "The7 14.2+. Requires WordPress 6.6+ and PHP 7.2+. Classic theme (NOT FSE)."
---

# The7 Theme Configuration

## Theme Type

**Classic theme (NOT Full Site Editing)**. All configuration is stored in `wp_options` table as a serialized array under option name `the7mk2`. Does NOT use Global Styles or theme.json. Uses a custom Options Framework with `of_get_option()` accessor.

## When to use

- The user wants to change colors, fonts, header, footer, or layout of The7
- The user wants to configure blog, portfolio, or sidebar settings
- The user wants to adjust buttons, page titles, or image hover effects
- The user wants to set up logo, favicons, and branding
- The user wants to set up the site identity

## Inputs required

- What aspect to configure (colors, typography, header, footer, layout, blog, buttons, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## Procedure

### 0) Verify the active theme

Call `mcm/theme-config-guide` — it auto-detects the active theme and confirms it is `dt-the7` (classic theme).

### 1) Read current configuration

```json
// Read ALL The7 options (auto-detects the7mk2)
mcm/get-theme-options {}

// Read specific options only
mcm/get-theme-options {
  "keys": [
    "general-layout",
    "general-content_width",
    "general-accent_bg_color",
    "footer-style",
    "sidebar-width"
  ]
}
```

### 2) Update a single option

```json
mcm/set-theme-options {"values": {"general-accent_bg_color": "#E94560"}}
```

### 3) Update multiple options at once

```json
mcm/set-theme-options {
  "values": {
    "general-layout": "wide",
    "general-content_width": "1200",
    "general-accent_bg_color": "#E94560",
    "general-bg_color": "#252525",
    "content-headers_color": "#252525",
    "content-primary_text_color": "#686868",
    "footer-style": "solid_background",
    "footer-bg_color": "#1B1B1B"
  }
}
// Dynamic CSS cache is automatically cleared after the update
```

### 4) Configure branding and logos

After uploading images with `mcm/upload-media`, update branding options:

```json
mcm/set-theme-options {
  "values": {
    "general-favicon": "https://example.com/wp-content/uploads/favicon.png",
    "general-favicon_hd": "https://example.com/wp-content/uploads/favicon@2x.png"
  }
}
```

### 5) Configure footer layout

The7 supports flexible footer column layouts:

```json
mcm/set-theme-options {
  "values": {
    "footer-style": "solid_background",
    "footer-bg_color": "#1B1B1B",
    "footer-layout": "1/4+1/4+1/4+1/4",
    "footer-headers_color": "#ffffff",
    "footer-primary_text_color": "#828282",
    "footer-padding": "50px 50px 50px 50px",
    "bottom_bar-enabled": "1",
    "bottom_bar-copyrights": "Copyright 2026 Your Company"
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

The `mcm/set-theme-options` ability automatically clears The7's compiled CSS transients and dynamic CSS cache after updating. No manual cache clearing is needed.

## Important: The7 Color System

The7 uses an **accent color** system with color mode switching:
- `general-accent_color_mode`: `color` or `gradient`
- When set to `color`: uses `general-accent_bg_color` (single hex value)
- When set to `gradient`: uses `general-accent_bg_color_gradient` (gradient definition)

Many options reference the accent color mode. Buttons, image hovers, and other elements can be set to `accent` mode (inherits global accent) or `color` mode (custom color).

## Verification

- [ ] Colors display correctly (accent, background, text, headers)
- [ ] Typography (body, headings, widgets) renders correctly
- [ ] Header layout and logo display correctly
- [ ] Footer style, colors, and columns are correct
- [ ] Page titles and breadcrumbs display correctly
- [ ] Blog and portfolio layouts work
- [ ] Button styles and sizes are correct
- [ ] Sidebar width and styling are correct
- [ ] Image hover effects work
- [ ] Dynamic CSS has been regenerated

## Failure modes / debugging

- **Changes not visible:** The MCP ability auto-clears The7's compiled CSS transients; clear browser cache if needed
- **Option not saving:** The `mcm/set-theme-options` ability reads the full `the7mk2` array before updating — it merges only the keys you specify
- **Spacing options:** Use format `"50px 50px 50px 50px"` (top right bottom left)
- **Typography options:** Complex array with `font_family`, `font_size`, `line_height`, `text_transform`, etc.
- **Footer layout:** Uses string format like `"1/4+1/4+1/4+1/4"` or `"1/3+1/3+1/3"`
- **Loading animation not changing:** Check `general-beautiful_loading` option (values: `enabled`, `disabled`)

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all option IDs with types and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared reference (see Section 0 for Classic vs FSE differences)
