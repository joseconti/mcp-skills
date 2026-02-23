---
name: theme-twentytwentyfour-config
description: "Use when configuring the Twenty Twenty-Four WordPress theme. Provides all available options (colors, typography, layout, spacing, duotones, gradients, templates, block styles) and procedures to apply them via MCP Content Manager abilities."
compatibility: "Twenty Twenty-Four 1.4+. Requires WordPress 6.4+ and PHP 7.0+. Block theme (FSE)."
---

# Twenty Twenty-Four Theme Configuration

## Theme Type

**Block theme (Full Site Editing)**. All visual configuration is stored in Global Styles (`wp_global_styles` post type), NOT in the Customizer or theme mods.

## When to use

- The user wants to change colors, fonts, spacing, or layout of Twenty Twenty-Four
- The user wants to apply duotone filters or gradients
- The user wants to switch between template variations (sidebar, wide image, etc.)
- The user wants to customize per-block styles (buttons, quotes, navigation, etc.)
- The user wants to set up the site identity (title, tagline, logo)

## Inputs required

- What aspect to configure (colors, typography, layout, templates, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## Procedure

### 0) Verify the active theme

Call `mcm/theme-config-guide` — it auto-detects the active theme and confirms it is `twentytwentyfour` (block theme).

### 1) Read current configuration

```json
// Read all Global Styles (settings + styles merged)
mcm/get-global-styles {"section": "both", "origin": "all"}

// Read only user customizations
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
          {"color": "#f9f9f9", "name": "Base", "slug": "base"},
          {"color": "#111111", "name": "Contrast", "slug": "contrast"},
          {"color": "#E94560", "name": "Accent 1", "slug": "accent-1"}
        ]
      }
    }
  }
}

// Change body typography
mcm/set-global-styles {
  "styles": {
    "typography": {
      "fontFamily": "var:preset|font-family|heading",
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

Twenty Twenty-Four provides several templates:

**Custom Templates:**
- `page-no-title` — Page without title (for pages)
- `page-with-sidebar` — Page with sidebar (for pages)
- `page-wide` — Page with wide image (for pages)
- `single-with-sidebar` — Single post with sidebar (for posts)

**Template Parts:**
- `header` — Site header
- `footer` — Site footer
- `sidebar` — Sidebar
- `post-meta` — Post metadata

To assign a template to a page, use `mcm/update-content` with the `template` field if supported, or update the page's `page_template` post meta.

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

- [ ] Colors display correctly (10-color palette)
- [ ] Typography renders as expected (Inter for body, Cardo for headings)
- [ ] Duotone filters work on images
- [ ] Gradients display correctly
- [ ] Layout widths (620px content, 1280px wide) are correct
- [ ] Header and footer display correctly
- [ ] Sidebar template works on pages and posts
- [ ] Button styles (default and outline) look right
- [ ] Responsive behavior works (fluid typography, spacing)

## Failure modes / debugging

- **Changes not visible:** Cache is automatically cleared by MCP abilities; clear browser cache if needed
- **Global Styles post not found:** Use `mcm/install-theme` with slug `twentytwentyfour` to install and activate
- **Font not loading:** Font slugs are `body` (Inter), `heading` (Cardo), `system-sans-serif`, `system-serif`
- **Color not applying:** Use `var:preset|color|{slug}` format (note: slugs use hyphens like `base-2`, `contrast-2`, `accent-3`)
- **Duotone not applying:** Duotone only works on images and cover blocks

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all configurable options with slugs and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared API reference for saving configuration
