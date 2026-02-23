---
name: theme-twentytwentyfive-config
description: "Use when configuring the Twenty Twenty-Five WordPress theme. Provides all available options (colors, typography, layout, spacing, templates, block styles) and procedures to apply them via MCP Content Manager abilities."
compatibility: "Twenty Twenty-Five 1.4+. Requires WordPress 6.7+ and PHP 7.2+. Block theme (FSE)."
---

# Twenty Twenty-Five Theme Configuration

## Theme Type

**Block theme (Full Site Editing)**. All visual configuration is stored in Global Styles (`wp_global_styles` post type), NOT in the Customizer or theme mods.

## When to use

- The user wants to change colors, fonts, spacing, or layout of Twenty Twenty-Five
- The user wants to switch between template/header/footer variations
- The user wants to customize per-block styles (buttons, quotes, navigation, etc.)
- The user wants to set up the site identity (title, tagline, logo)

## Inputs required

- What aspect to configure (colors, typography, layout, templates, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## Procedure

### 0) Verify the active theme

Call `mcm/theme-config-guide` — it auto-detects the active theme and confirms it is `twentytwentyfive` (block theme).

### 1) Read current configuration

```json
// Read all Global Styles (settings + styles merged)
mcm/get-global-styles {"section": "both", "origin": "all"}

// Read only user customizations (overrides over theme.json defaults)
mcm/get-global-styles {"section": "both", "origin": "user"}

// Read only color settings
mcm/get-global-styles {"section": "settings", "path": "color.palette"}

// Read only typography styles
mcm/get-global-styles {"section": "styles", "path": "typography"}
```

### 2) Apply configuration changes

See [references/theme-options.md](references/theme-options.md) for all available options with exact slugs and default values.

See [../global-styles-api.md](../global-styles-api.md) for the full API reference.

**General pattern for updating Global Styles:**

```json
// Change background and text colors (deep merge — other settings remain intact)
mcm/set-global-styles {
  "styles": {
    "color": {
      "background": "var:preset|color|contrast",
      "text": "var:preset|color|base"
    }
  }
}

// Change the color palette
mcm/set-global-styles {
  "settings": {
    "color": {
      "palette": {
        "theme": [
          {"color": "#FFFFFF", "name": "Base", "slug": "base"},
          {"color": "#1A1A2E", "name": "Contrast", "slug": "contrast"},
          {"color": "#E94560", "name": "Accent 1", "slug": "accent-1"},
          {"color": "#F6CFF4", "name": "Accent 2", "slug": "accent-2"},
          {"color": "#503AA8", "name": "Accent 3", "slug": "accent-3"},
          {"color": "#686868", "name": "Accent 4", "slug": "accent-4"},
          {"color": "#FBFAF3", "name": "Accent 5", "slug": "accent-5"},
          {"color": "color-mix(in srgb, currentColor 20%, transparent)", "name": "Accent 6", "slug": "accent-6"}
        ]
      }
    }
  }
}

// Change body typography
mcm/set-global-styles {
  "styles": {
    "typography": {
      "fontFamily": "var:preset|font-family|fira-code",
      "fontSize": "var:preset|font-size|medium",
      "fontWeight": "400",
      "lineHeight": "1.6"
    }
  }
}

// Change layout widths
mcm/set-global-styles {
  "settings": {
    "layout": {
      "contentSize": "720px",
      "wideSize": "1200px"
    }
  }
}
```

### 3) Configure templates and template parts

Twenty Twenty-Five provides multiple header and footer variations:

**Headers:**
- `header` — Default header
- `vertical-header` — Vertical site header
- `header-large-title` — Header with large title

**Footers:**
- `footer` — Default footer
- `footer-columns` — Footer with columns
- `footer-newsletter` — Footer with newsletter

**Other parts:**
- `sidebar` — Sidebar

To switch a template part, use `mcm/search-content` to find the template, then `mcm/update-content` to modify the block content (replace the header/footer slug reference in the template's block markup).

### 4) Set up site identity

```json
mcm/set-option {"name": "blogname", "value": "Site Name"}
mcm/set-option {"name": "blogdescription", "value": "Site Tagline"}
mcm/set-theme-mod {"key": "custom_logo", "value": <attachment_id>}
mcm/set-option {"name": "site_icon", "value": <attachment_id>}
mcm/set-option {"name": "show_on_front", "value": "page"}
mcm/set-option {"name": "page_on_front", "value": <page_id>}
mcm/set-option {"name": "page_for_posts", "value": <page_id>}
```

## Verification

- [ ] Colors display correctly on the frontend
- [ ] Typography (font family, sizes, weights) renders as expected
- [ ] Layout widths (content/wide) are correct
- [ ] Header and footer variations are correct
- [ ] Navigation links work
- [ ] Site title and tagline display correctly
- [ ] Button styles (default and outline) look right
- [ ] Responsive behavior works (fluid typography, spacing)

## Failure modes / debugging

- **Changes not visible:** Cache is automatically cleared by MCP abilities; clear browser cache if needed
- **Global Styles post not found:** The theme may not have been activated yet; use `mcm/install-theme` with slug `twentytwentyfive` to install and activate
- **Font not loading:** Ensure the font slug matches exactly (e.g., `manrope`, `fira-code`)
- **Color not applying:** Use the `var:preset|color|{slug}` format, not raw hex values, when referencing palette colors in styles

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all configurable options with slugs and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared API reference for saving configuration
