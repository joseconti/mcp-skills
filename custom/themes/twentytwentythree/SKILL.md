---
name: twentytwentythree
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

## AI-Guided Configuration Workflow

When configuring Twenty Twenty-Three, offer the user **two modes**:

### Mode 1: "Guide me step by step"

Ask the user about each configuration area, one at a time:

1. **Style Variation**: "Twenty Twenty-Three comes with **10 pre-built style variations**, each with a completely different look. Would you like to start with one of these as a base?
   - **Default** — Lime green accents on white, System Font, minimal and clean
   - **Aubergine** — Dark purple base with coral accents, DM Sans, rounded gradient buttons
   - **Block Out** — Bold bright red base, IBM Plex Mono italic headings, duotone images
   - **Canary** — Bright yellow background, full monospace (IBM Plex Mono), compact layout
   - **Electric** — Electric blue on off-white, DM Sans, sharp modern feel
   - **Grapes** — Light beige with dark green accents, Source Serif Pro headings, organic feel
   - **Marigold** — Warm beige with purple-brown and yellow, Source Serif Pro body, italic headings
   - **Pilgrimage** — Dark gray with green/cyan/lime neon, gradient dots background
   - **Pitch** — Very dark gray with tan/brown, Inter font, responsive width, square buttons
   - **Sherbet** — White with magenta/yellow/cyan pastels, rounded uppercase buttons
   - **Whisper** — Purple-gray with deep red accents, shadow buttons, bordered root
   Pick one, or I can customize from scratch."

2. **Colors**: "What are your brand colors? The theme uses 5 color slots:
   - **Base** — Main background (default: white)
   - **Contrast** — Main text (default: black)
   - **Primary** — Accent/buttons (default: lime green #9DFF20)
   - **Secondary** — Secondary accent (default: dark green #345C00)
   - **Tertiary** — Subtle backgrounds (default: light gray #F6F6F6)"

3. **Typography**: "What fonts do you prefer? Available: DM Sans (sans-serif, 400/700), IBM Plex Mono (monospace, 300/400/700), Inter (sans-serif, 200–900), Source Serif Pro (serif, 200–900), or System Font (default). Pick one for body text and one for headings."

4. **Layout**: "What content width? Default is 650px (narrow, good for reading). Wide is 1200px. Want to adjust?"

5. **Buttons**: "Default buttons are lime green with sharp corners. Want rounded? Different color? Different hover effects?"

6. **Site identity**: "What is your site name and tagline? Do you have a logo and favicon?"

### Mode 2: "Design it for me"

1. Ask: site type (blog, portfolio, creative, corporate, etc.), brand color (if any), general feel (modern, elegant, bold, minimal, warm)
2. Select the best style variation as base, then customize colors and fonts
3. Apply all settings in one batch
4. Tell the user exactly what was configured

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

Twenty Twenty-Three ships with **10 style variations**. Each completely redefines colors, and many also change fonts, button styles, layout widths, and element appearances. See [references/theme-options.md](references/theme-options.md) for the full color palette and key changes of each variation.

To apply a style variation:

```json
// Get available variations from the style_variations field
mcm/get-global-styles {"section": "both"}

// Apply a variation (use merge_mode replace to fully switch)
mcm/set-global-styles {
  "settings": { /* variation's settings */ },
  "styles": { /* variation's styles */ },
  "merge_mode": "replace"
}
```

**Note:** When applying a style variation, use `merge_mode: "replace"` to fully replace the current styles. Otherwise, remnants of previous customizations may persist.

### 4) Configure templates

**Custom Templates:**
- `blank` — Empty template (for pages and posts)
- `blog-alternative` — Alternative blog layout (for pages)
- `404` — Custom 404 page (for pages)

**Default Templates:** index.html (blog), home.html (homepage), archive.html, search.html, single.html (post), page.html, 404.html, blog-alternative.html

**Template Parts:**
- `header` — Site header (site title + navigation)
- `footer` — Site footer (delegates to footer-default pattern)
- `comments` — Comments template part (delegates to hidden-comments pattern)
- `post-meta` — Post metadata (delegates to post-meta pattern)

### 5) Block Patterns

**Visible patterns (in block inserter):**
- `twentytwentythree/footer-default` — Footer with site title and powered-by text
- `twentytwentythree/post-meta` — Post date, category, author, tags with separator
- `twentytwentythree/cta` — Call to action with button and separator

**Hidden patterns (used internally):**
- `twentytwentythree/hidden-comments` — Full comments section with threading
- `twentytwentythree/hidden-404` — 404 heading + message + search form
- `twentytwentythree/hidden-no-results-content` — No results + search form
- `twentytwentythree/hidden-heading` — Homepage heading

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

- [ ] Colors display correctly (5-color palette: base, contrast, primary, secondary, tertiary)
- [ ] Typography renders as expected (System Font by default, 5 available font families)
- [ ] Layout widths (650px content, 1200px wide) are correct
- [ ] Button styling works (lime green primary, sharp corners)
- [ ] Link states work (underline, hover, focus with dashed underline, active)
- [ ] Style variations apply correctly if used
- [ ] Header and footer display correctly
- [ ] Responsive behavior works (fluid typography, spacing)
- [ ] Per-block styles (navigation, quotes, pullquotes, comments, separator) display correctly

## Failure modes / debugging

- **Changes not visible:** Cache is automatically cleared by MCP abilities; clear browser cache if needed
- **Global Styles post not found:** Use `mcm/install-theme` with slug `twentytwentythree` to install and activate
- **Font not loading:** Font slugs are `dm-sans`, `ibm-plex-mono`, `inter`, `system-font`, `source-serif-pro`
- **Color not applying:** Use `var:preset|color|{slug}` (slugs: `base`, `contrast`, `primary`, `secondary`, `tertiary`)
- **Style variations not showing:** Ensure theme files are intact; variations are in the `styles/` directory
- **Drop cap not working:** Drop cap is intentionally disabled in this theme (`"dropCap": false`)
- **Spacing not responsive:** Spacing sizes use `clamp()` formulas — they scale with viewport width automatically

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all configurable options with slugs and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared API reference for saving configuration
