---
name: twentytwentyfive
description: "Use when configuring the Twenty Twenty-Five WordPress theme. Provides all available options (colors, typography, layout, spacing, templates, block styles, 8 style variations, 98 patterns) and procedures to apply them via MCP Content Manager abilities."
compatibility: "Twenty Twenty-Five 1.4+. Requires WordPress 6.7+ and PHP 7.2+. Block theme (FSE)."
---

# Twenty Twenty-Five Theme Configuration

## Theme Type

**Block theme (Full Site Editing)**. All visual configuration is stored in Global Styles (`wp_global_styles` post type), NOT in the Customizer or theme mods.

## When to use

- The user wants to change colors, fonts, spacing, or layout of Twenty Twenty-Five
- The user wants to switch between style variations (8 available)
- The user wants to switch between template/header/footer variations
- The user wants to customize per-block styles (buttons, quotes, navigation, etc.)
- The user wants to use block patterns for page layouts (98 available)
- The user wants to set up the site identity (title, tagline, logo)

## Inputs required

- What aspect to configure (colors, typography, layout, templates, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## AI-Guided Configuration Workflow

When configuring Twenty Twenty-Five, offer the user **two modes**:

### Mode 1: "Guide me step by step"

Ask the user about each configuration area:

1. **Style Variation**: "Twenty Twenty-Five comes with **8 pre-built style variations**, each with a completely different look. Would you like to start with one?
   - **Default** — Clean white base, yellow/pink/purple accents, Manrope sans-serif, light weight (300)
   - **Evening** — Dark theme (#1B1B1B), olive/purple accents, Manrope font
   - **Noon** — Elegant cream base, peach accents, Literata serif body + Beiruti sans buttons
   - **Dusk** — Light gray, vibrant purple accents, Fira Code monospace body + Vollkorn serif headings
   - **Afternoon** — Nature green/sage palette, Ysabeau Office body + Platypi headings, sharp buttons
   - **Twilight** — Very dark with blue/coral accents, Roboto Slab headings, uppercase navigation
   - **Morning** — Beige/tan with soft blue accents, Ysabeau Office body + Literata headings (weight 900)
   - **Sunrise** — Dark burgundy with rose/yellow accents, Literata body (1.5rem) + Platypi headings (weight 800)
   - **Midnight** — Deep purple with neon cyan, cyberpunk style, duotone images, Fira Sans body + Literata headings
   Pick one, or customize from scratch."

2. **Colors**: "The theme uses **8 color slots**:
   - **Base** — Main background (default: white)
   - **Contrast** — Main text (default: near-black)
   - **Accent 1** — Primary accent (default: yellow)
   - **Accent 2** — Secondary accent (default: light pink)
   - **Accent 3** — Tertiary accent (default: purple)
   - **Accent 4** — Subdued text (default: gray — used for dates, secondary text)
   - **Accent 5** — Subtle background (default: off-white)
   - **Accent 6** — Dynamic (20% of current text color — used for borders, separators)
   What are your brand colors?"

3. **Typography**: "Default: Manrope (light weight 300) for body, same for headings. Also available: Fira Code (monospace). Style variations add 7 more fonts: Beiruti, Literata, Vollkorn, Platypi, Ysabeau Office, Roboto Slab, Fira Sans."

4. **Header/Footer**: "Three header options:
   - **Default** — Standard header with title + navigation
   - **Vertical** — Sidebar-style vertical header
   - **Large Title** — Prominent title header
   Three footer options:
   - **Default** — Standard footer
   - **Columns** — Multi-column footer layout
   - **Newsletter** — Footer with newsletter signup
   Which combination do you prefer?"

5. **Blog Style**: "The theme includes patterns for 4 blog styles:
   - **News blog** — Traditional news layout
   - **Photo blog** — Visual/photography focused
   - **Text blog** — Text-focused, minimal
   - **Vertical header blog** — Blog with sidebar navigation
   Each has matching home, single, archive, and search templates."

6. **Page Layouts**: "Need specific page layouts? Available patterns include:
   - Business/portfolio/shop home pages
   - Landing pages (book, event, podcast, coming soon)
   - Link-in-bio pages (3 variants)
   - CV/bio page
   - Hero sections, banners, pricing tables, testimonials, event schedules"

7. **Site identity**: "What is your site name, tagline, logo, and favicon?"

### Mode 2: "Design it for me"

1. Ask: site type, brand color (if any), general feel (modern, elegant, bold, minimal, warm, dark, tech)
2. Select the best style variation as base
3. Choose matching header/footer combination
4. Apply all settings in one batch
5. Tell the user what was configured and why

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

### 3) Style Variations

Twenty Twenty-Five ships with **8 style variations** (Evening, Noon, Dusk, Afternoon, Twilight, Morning, Sunrise, Midnight). Each provides unique colors and most introduce new fonts. See [references/theme-options.md](references/theme-options.md) for details.

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

**Note:** Each variation defines section variations (`section-1` through `section-5`) that apply different colors to Group blocks using `.is-style-section-N` classes.

### 4) Configure templates and template parts

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

To switch a template part, use `mcm/search-content` to find the template, then `mcm/update-content` to modify the block content.

### 5) Block Patterns (98 patterns)

The theme includes 98 patterns organized by use case:

- **Headers** (5): default, vertical, large-title, centered, columns
- **Footers** (5): default, columns, newsletter, centered, social
- **Blog query loops** (5): standard, text, photo, news, vertical-header
- **Template variants** (30+): home/single/archive/search for each blog style
- **Hero/Banner** (7): full-width, book, podcast, intro, poster
- **CTA/Marketing** (7): centered, newsletter, events, book links
- **Business sections**: services, team, pricing, testimonials, events
- **Landing pages** (8): book, event, podcast, coming-soon, CV/bio, link-in-bio
- **Hidden/Utility** (8): blog-heading, search, 404, written-by, sidebar, navigation, comments, more-posts

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

- [ ] Colors display correctly on the frontend
- [ ] Typography (font family, sizes, weights) renders as expected
- [ ] Layout widths (content/wide) are correct
- [ ] Header and footer variations are correct
- [ ] Navigation links work
- [ ] Site title and tagline display correctly
- [ ] Button styles (default and outline) look right
- [ ] Style variation applied correctly (if used)
- [ ] Blog query patterns display posts correctly
- [ ] Section variations display different colors (if used)
- [ ] Responsive behavior works (fluid typography, spacing)

## Failure modes / debugging

- **Changes not visible:** Cache is automatically cleared by MCP abilities; clear browser cache if needed
- **Global Styles post not found:** The theme may not have been activated yet; use `mcm/install-theme` with slug `twentytwentyfive` to install and activate
- **Font not loading:** Base fonts: `manrope`, `fira-code`. Variation fonts are only available when that variation is active.
- **Color not applying:** Use the `var:preset|color|{slug}` format, not raw hex values. Accent 6 is dynamic — it uses `color-mix()`.
- **Section variations not working:** Apply with Group block using `.is-style-section-N` class. Only available when a style variation defines them.
- **Duotone not working:** Only the Midnight variation defines duotone filters.
- **Pattern not found:** Use `twentytwentyfive/` prefix (e.g., `twentytwentyfive/hero-full-width-image`)

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all configurable options with slugs and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared API reference for saving configuration
