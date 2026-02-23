---
name: twentytwentyfour
description: "Use when configuring the Twenty Twenty-Four WordPress theme. Provides all available options (colors, typography, layout, spacing, duotones, gradients, templates, block styles, style variations, patterns) and procedures to apply them via MCP Content Manager abilities."
compatibility: "Twenty Twenty-Four 1.4+. Requires WordPress 6.4+ and PHP 7.0+. Block theme (FSE)."
---

# Twenty Twenty-Four Theme Configuration

## Theme Type

**Block theme (Full Site Editing)**. All visual configuration is stored in Global Styles (`wp_global_styles` post type), NOT in the Customizer or theme mods.

## When to use

- The user wants to change colors, fonts, spacing, or layout of Twenty Twenty-Four
- The user wants to apply duotone filters or gradients
- The user wants to switch between style variations (7 available)
- The user wants to switch between template variations (sidebar, wide image, etc.)
- The user wants to customize per-block styles (buttons, quotes, navigation, etc.)
- The user wants to use block patterns for page layouts
- The user wants to set up the site identity (title, tagline, logo)

## Inputs required

- What aspect to configure (colors, typography, layout, templates, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## AI-Guided Configuration Workflow

When configuring Twenty Twenty-Four, offer the user **two modes**:

### Mode 1: "Guide me step by step"

Ask the user about each configuration area:

1. **Style Variation**: "Twenty Twenty-Four comes with **7 pre-built style variations**. Would you like to start with one?
   - **Default** — Warm neutrals (beige/sandstone/rust/sage), Inter body + Cardo serif headings
   - **Fossil** — Earth tones (brown/neutral), fonts SWAPPED (Inter headings, Cardo body), pill-shaped buttons
   - **Ice** — Cool blue palette, Inter headings + Jost body, uppercase buttons with letter-spacing
   - **Maelstrom** — Dark blue background with white text, Cardo body + Jost headings
   - **Mint** — Light mint/green, Instrument Sans headings + Jost body, modern sans-serif
   - **Rust** — Minimal rust/earth palette with transparent gradients
   - **Ember** — Warm orange, Instrument Sans body + Jost headings, default duotone on images
   - **Onyx** — Dark mode with 10-color palette, 5 duotones, wood/earth accents
   Pick one, or customize from scratch."

2. **Colors**: "The theme uses **10 color slots**:
   - **Base / Base 2** — Background colors (light gray / white)
   - **Contrast / Contrast 2 / Contrast 3** — Text colors (dark / medium gray / light gray)
   - **Accent / Accent 2-5** — Accent colors (beige / sandstone / rust / sage / mint)
   What are your brand colors?"

3. **Typography**: "Default: Inter for body, Cardo (serif) for headings. Also available: System Sans-serif and System Serif. What fonts do you prefer?"

4. **Layout**: "Content width: 620px (narrow reading width), Wide: 1280px. Want to adjust?"

5. **Templates**: "Which page templates do you need?
   - **Page with Sidebar** — Content + sidebar layout
   - **Page Wide** — Hero image layout
   - **Page No Title** — Clean page without title
   - **Single with Sidebar** — Blog post with sidebar"

6. **Patterns**: "The theme includes **57 patterns** for page layouts. Key ones:
   - Banner/hero sections (full-width images with CTAs)
   - 3-column blog grids
   - Services and team grids
   - Testimonials, pricing tables
   - Portfolio layouts
   Want me to set up any specific page layouts?"

7. **Site identity**: "What is your site name, tagline, logo, and favicon?"

### Mode 2: "Design it for me"

1. Ask: site type, brand color (if any), general feel
2. Select the best style variation as base
3. Apply all settings in one batch
4. Tell the user what was configured and why

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
          {"color": "#E94560", "name": "Accent", "slug": "accent"}
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

### 3) Style Variations

Twenty Twenty-Four ships with **7 style variations** (Fossil, Ice, Maelstrom, Mint, Rust, Ember, Onyx). Each provides unique colors, and some introduce new fonts (Jost, Instrument Sans). See [references/theme-options.md](references/theme-options.md) for details.

```json
// Get available variations
mcm/get-global-styles {"section": "both"}

// Apply a variation (use merge_mode replace)
mcm/set-global-styles {
  "settings": { /* variation's settings */ },
  "styles": { /* variation's styles */ },
  "merge_mode": "replace"
}
```

### 4) Configure templates and template parts

**Custom Templates:**
- `page-no-title` — Page without title (for pages)
- `page-with-sidebar` — Page with sidebar (for pages)
- `page-wide` — Page with wide image (for pages)
- `single-with-sidebar` — Single post with sidebar (for posts)

**Default Templates:** page.html, single.html, home.html, index.html, archive.html, search.html, 404.html

**Template Parts:**
- `header` — Site header (logo + site title + navigation)
- `footer` — Site footer (4-column layout with nav, colophon)
- `sidebar` — Sidebar (hidden-sidebar pattern)
- `post-meta` — Post metadata (hidden-post-meta pattern)

### 5) Block Patterns (57 patterns)

The theme includes 57 patterns across categories: banners, CTAs, galleries, post grids, page layouts, team/testimonials, footers, and hidden utility patterns. Key patterns:

- `posts-3-col` — 3-column blog grid (used by index, archive, search)
- `page-home-business` — Business homepage (used by home.html)
- `banner-hero` — Full-width hero section
- `footer` — 4-column footer layout
- `hidden-comments` — Comments section
- `hidden-post-navigation` — Post navigation

### 6) Set up site identity

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
- [ ] Custom block styles work (arrow-icon-details, pill terms, checkmark-list, arrow-link, asterisk heading)
- [ ] Style variations apply correctly if used
- [ ] Responsive behavior works (fluid typography, spacing)

## Failure modes / debugging

- **Changes not visible:** Cache is automatically cleared by MCP abilities; clear browser cache if needed
- **Global Styles post not found:** Use `mcm/install-theme` with slug `twentytwentyfour` to install and activate
- **Font not loading:** Font slugs are `body` (Inter), `heading` (Cardo), `system-sans-serif`, `system-serif`
- **Color not applying:** Use `var:preset|color|{slug}` format (note: slugs use hyphens like `base-2`, `contrast-2`, `accent-3`)
- **Duotone not applying:** Duotone only works on images and cover blocks
- **Pattern not found:** Use `twentytwentyfour/` prefix (e.g., `twentytwentyfour/posts-3-col`)
- **Block style not showing:** Custom block styles registered in functions.php: `arrow-icon-details`, `pill`, `checkmark-list`, `arrow-link`, `asterisk`

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all configurable options with slugs and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared API reference for saving configuration
