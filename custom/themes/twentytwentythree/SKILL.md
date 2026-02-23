---
name: theme-twentytwentythree-config
description: "Use when configuring the Twenty Twenty-Three WordPress theme. Provides all available options (colors, typography, layout, spacing, templates, block styles, style variations) and procedures to apply them via MCP Content Manager abilities."
compatibility: "Twenty Twenty-Three 1.6+. Requires WordPress 6.1+ and PHP 5.6+. Block theme (FSE)."
---

# Twenty Twenty-Three Theme Configuration

## Theme Type

**Block theme (Full Site Editing)**. All visual configuration is stored in Global Styles (`wp_global_styles` post type), NOT in the Customizer or theme mods.

## When to use

- The user wants to change colors, fonts, spacing, or layout of Twenty Twenty-Three
- The user wants to switch between style variations
- The user wants to customize per-block styles (buttons, quotes, navigation, etc.)
- The user wants to set up the site identity (title, tagline, logo)

## Inputs required

- What aspect to configure (colors, typography, layout, templates, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## Procedure

### 0) Verify the active theme

Call `mcm/theme-config-guide` — it auto-detects the active theme and confirms it is `twentytwentythree` (block theme).

### 1) Read current configuration

```json
// Read all Global Styles (settings + styles merged)
mcm/get-global-styles {"section": "both", "origin": "all"}

// Read only user customizations
mcm/get-global-styles {"section": "both", "origin": "user"}

// Read only color settings
mcm/get-global-styles {"section": "settings", "path": "color.palette"}

// Read available style variations (included in the response)
mcm/get-global-styles {"section": "both"}
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
      "background": "var:preset|color|base",
      "text": "var:preset|color|contrast"
    }
  }
}

// Change the color palette
mcm/set-global-styles {
  "settings": {
    "color": {
      "palette": {
        "theme": [
          {"color": "#ffffff", "name": "Base", "slug": "base"},
          {"color": "#000000", "name": "Contrast", "slug": "contrast"},
          {"color": "#9DFF20", "name": "Primary", "slug": "primary"},
          {"color": "#345C00", "name": "Secondary", "slug": "secondary"},
          {"color": "#F6F6F6", "name": "Tertiary", "slug": "tertiary"}
        ]
      }
    }
  }
}

// Change body typography
mcm/set-global-styles {
  "styles": {
    "typography": {
      "fontFamily": "var:preset|font-family|inter",
      "fontSize": "var:preset|font-size|medium",
      "lineHeight": "1.6"
    }
  }
}
```

### 3) Style Variations

Twenty Twenty-Three ships with **10 style variations** in its `styles/` directory. These offer pre-made combinations of colors and fonts. The `mcm/get-global-styles` response includes available style variations when the theme supports them.

To apply a style variation, use `mcm/set-global-styles` with the variation's settings and styles objects. First read the available variations from the `style_variations` field in the `mcm/get-global-styles` response, then apply the desired one:

```json
// Apply a style variation by passing its settings and styles
// (get the exact data from the style_variations list first)
mcm/set-global-styles {
  "settings": { /* variation's settings */ },
  "styles": { /* variation's styles */ },
  "merge_mode": "replace"
}
```

**Note:** When applying a style variation, use `merge_mode: "replace"` to fully replace the current styles with the variation's styles. Otherwise, remnants of the previous customization may persist.

### 4) Configure templates

**Custom Templates:**
- `blank` — Empty template (for pages and posts)
- `blog-alternative` — Alternative blog layout (for pages)
- `404` — Custom 404 page (for pages)

**Template Parts:**
- `header` — Site header
- `footer` — Site footer
- `comments` — Comments template part
- `post-meta` — Post metadata

### 5) Set up site identity

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

- [ ] Colors display correctly (5-color palette: base, contrast, primary, secondary, tertiary)
- [ ] Typography renders as expected (System Font by default, 5 available font families)
- [ ] Layout widths (650px content, 1200px wide) are correct
- [ ] Button styling works (lime green primary, sharp corners)
- [ ] Link states work (underline, hover, focus with dashed underline, active)
- [ ] Style variations apply correctly if used
- [ ] Header and footer display correctly
- [ ] Responsive behavior works (fluid typography, spacing)

## Failure modes / debugging

- **Changes not visible:** Cache is automatically cleared by MCP abilities; clear browser cache if needed
- **Global Styles post not found:** Use `mcm/install-theme` with slug `twentytwentythree` to install and activate
- **Font not loading:** Font slugs are `dm-sans`, `ibm-plex-mono`, `inter`, `system-font`, `source-serif-pro`
- **Color not applying:** Use `var:preset|color|{slug}` (slugs: `base`, `contrast`, `primary`, `secondary`, `tertiary`)
- **Style variations not showing:** Ensure theme files are intact; variations are in the `styles/` directory
- **Drop cap not working:** Drop cap is intentionally disabled in this theme (`"dropCap": false`)

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all configurable options with slugs and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared API reference for saving configuration
