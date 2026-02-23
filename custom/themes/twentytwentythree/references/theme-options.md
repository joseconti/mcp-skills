# Twenty Twenty-Three — Complete Configurable Options

All values below are the **theme.json defaults**. User overrides are stored in Global Styles (`wp_global_styles` post type). Use `var:preset|{type}|{slug}` format to reference presets in styles.

---

## Global Settings

| Setting | Value | Description |
|---------|-------|-------------|
| `$schema` | `https://schemas.wp.org/wp/6.5/theme.json` | Theme.json schema version |
| `version` | `2` | Theme.json spec version |
| `appearanceTools` | `true` | Enables all appearance editing tools (border, spacing, dimensions, etc.) |
| `useRootPaddingAwareAlignments` | `true` | Full-width blocks honor root padding |
| `typography.dropCap` | `false` | Drop caps intentionally disabled |
| `typography.fluid` | `true` | Responsive fluid typography enabled globally |
| `spacing.spacingScale.steps` | `0` | Custom spacing scale (no auto-generation) |
| `spacing.units` | `%`, `px`, `em`, `rem`, `vh`, `vw` | Allowed CSS units for spacing |

---

## Color Palette

| Name | Slug | Default | CSS Variable |
|------|------|---------|-------------|
| Base | `base` | `#ffffff` | `--wp--preset--color--base` |
| Contrast | `contrast` | `#000000` | `--wp--preset--color--contrast` |
| Primary | `primary` | `#9DFF20` | `--wp--preset--color--primary` |
| Secondary | `secondary` | `#345C00` | `--wp--preset--color--secondary` |
| Tertiary | `tertiary` | `#F6F6F6` | `--wp--preset--color--tertiary` |

**Default styles:** Background = `base`, Text = `contrast`

**Notes:** No default duotone or gradient presets in the base theme. 5-color palette is intentionally minimal — style variations add their own palettes, duotones, and gradients.

### To change a color

```json
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
```

---

## Typography

### Font Families

| Name | Slug | Font Stack | Weight Range | Italic | Type |
|------|------|-----------|-------------|--------|------|
| DM Sans | `dm-sans` | `"DM Sans", sans-serif` | 400, 700 | Yes (400i, 700i) | Sans-serif |
| IBM Plex Mono | `ibm-plex-mono` | `'IBM Plex Mono', monospace` | 300, 400, 700 | Yes (400i) | Monospace |
| Inter | `inter` | `"Inter", sans-serif` | 200–900 (variable) | No | Sans-serif (variable) |
| System Font | `system-font` | System stack | — | — | Fallback |
| Source Serif Pro | `source-serif-pro` | `"Source Serif Pro", serif` | 200–900 (variable) | Yes (200–900i) | Serif (variable) |

**Default body font:** `system-font`

**Drop Cap:** Disabled (`"dropCap": false`)

### Font Sizes

| Name | Slug | Default Size | Fluid Min | Fluid Max | CSS Variable |
|------|------|-------------|-----------|-----------|-------------|
| Small | `small` | `1rem` | `0.875rem` | `1rem` | `--wp--preset--font-size--small` |
| Medium | `medium` | `1.125rem` | `1rem` | `1.125rem` | `--wp--preset--font-size--medium` |
| Large | `large` | `1.75rem` | `1.75rem` | `1.875rem` | `--wp--preset--font-size--large` |
| Extra Large | `x-large` | `2.25rem` | — (fixed) | — | `--wp--preset--font-size--x-large` |
| Extra Extra Large | `xx-large` | `10rem` | `6.1rem` | `10rem` | `--wp--preset--font-size--xx-large` |

### Default Body Typography

| Property | Value | Reference |
|----------|-------|-----------|
| Font Family | System Font | `var:preset|font-family|system-font` |
| Font Size | Medium | `var:preset|font-size|medium` |
| Line Height | 1.6 | — |

### Heading Typography

| Property | Value |
|----------|-------|
| Font Weight | 400 |
| Line Height | 1.4 |

| Heading | Font Size | Additional |
|---------|-----------|------------|
| H1 | `3.625rem` | line-height: 1.2 |
| H2 | `clamp(2.625rem, calc(2.625rem + ((1vw - 0.48rem) * 8.4135)), 3.25rem)` | line-height: 1.2 |
| H3 | `var:preset|font-size|x-large` | — |
| H4 | `var:preset|font-size|large` | — |
| H5 | `var:preset|font-size|medium` | weight: 700, uppercase |
| H6 | `var:preset|font-size|medium` | uppercase |

---

## Layout

| Property | Value |
|----------|-------|
| Content Size | 650px |
| Wide Size | 1200px |

---

## Spacing

### Spacing Scale

| Name | Slug | Default Size | CSS Variable |
|------|------|-------------|-------------|
| 1 | `30` | `clamp(1.5rem, 5vw, 2rem)` | `--wp--preset--spacing--30` |
| 2 | `40` | `clamp(1.8rem, 1.8rem + ((1vw - 0.48rem) * 2.885), 3rem)` | `--wp--preset--spacing--40` |
| 3 | `50` | `clamp(2.5rem, 8vw, 4.5rem)` | `--wp--preset--spacing--50` |
| 4 | `60` | `clamp(3.75rem, 10vw, 7rem)` | `--wp--preset--spacing--60` |
| 5 | `70` | `clamp(5rem, 5.25rem + ((1vw - 0.48rem) * 9.096), 8rem)` | `--wp--preset--spacing--70` |
| 6 | `80` | `clamp(7rem, 14vw, 11rem)` | `--wp--preset--spacing--80` |

**Default spacing:**
- Block Gap: `1.5rem`
- Root Padding: top/bottom `spacing-40`, left/right `spacing-30`

**Allowed units:** `%`, `px`, `em`, `rem`, `vh`, `vw`

---

## Templates & Template Parts

### Custom Templates

| Title | Slug | Post Types |
|-------|------|-----------|
| Blank | `blank` | page, post |
| Blog (Alternative) | `blog-alternative` | page |
| 404 | `404` | page |

### Default Templates

| File | Purpose | Key Content |
|------|---------|-------------|
| `index.html` | Blog listing | Query loop with post-template, pagination |
| `home.html` | Homepage | Alternative blog with columns, CTA pattern |
| `archive.html` | Archive/category | Query title + post listing + pagination |
| `search.html` | Search results | Query title + search form + post listing |
| `single.html` | Single post | Featured image, title, content, post-meta, comments |
| `page.html` | Single page | Featured image, title, content, comments |
| `blank.html` | Custom blank | Post content only (constrained) |
| `404.html` | Error page | Header + 404 pattern + footer |
| `blog-alternative.html` | Alternative blog | Minimal columns layout with date + title |

### Template Parts

| Title | Slug | Area | Content |
|-------|------|------|---------|
| Header | `header` | header | Site title (level 0) + Navigation (flex), padding-bottom spacing-40 |
| Footer | `footer` | footer | Delegates to `twentytwentythree/footer-default` pattern |
| Comments | `comments` | uncategorized | Delegates to `twentytwentythree/hidden-comments` pattern |
| Post Meta | `post-meta` | uncategorized | Delegates to `twentytwentythree/post-meta` pattern |

---

## Block Patterns

### Visible Patterns (shown in inserter)

| Title | Slug | Category | Description |
|-------|------|----------|-------------|
| Default Footer | `twentytwentythree/footer-default` | footer | Site title + "Powered by WordPress" text |
| Post Meta | `twentytwentythree/post-meta` | query | Date, category, author, tags with separator |
| Call to Action | `twentytwentythree/cta` | featured | Left-aligned text with CTA button and separator |

### Hidden Patterns (used internally by templates)

| Title | Slug | Used By |
|-------|------|---------|
| Comments | `twentytwentythree/hidden-comments` | comments template part |
| 404 | `twentytwentythree/hidden-404` | 404 template |
| No Results | `twentytwentythree/hidden-no-results-content` | search template |
| Heading | `twentytwentythree/hidden-heading` | home template |

---

## Style Variations (10 Pre-Built Designs)

Each variation completely redefines the color palette, and often changes fonts, button styles, and element appearances. Apply via `mcm/set-global-styles` with `merge_mode: "replace"`.

### 1. Aubergine

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#1B1031` (dark purple) |
| Contrast | `contrast` | `#FFFFFF` |
| Primary | `primary` | `#FF746D` (coral) |
| Secondary | `secondary` | `#551C5E` (purple) |
| Tertiary | `tertiary` | `#FB326B` (pink) |

**Key changes:** DM Sans body font, navigation medium size, buttons rounded (99999px) with gradient (tertiary→primary), site title uppercase with bottom border, italic post author/date/terms. 4 custom gradients.

### 2. Block Out

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#ff5252` (bright red) |
| Contrast | `contrast` | `#252525` (dark gray) |
| Primary | `primary` | `#ffffff` |
| Secondary | `secondary` | `#ff2d34` (red) |
| Tertiary | `tertiary` | `#ff7e7e` (light red) |

**Key changes:** Content width → 800px, xx-large → 7rem, site title xx-large italic lowercase, navigation large, IBM Plex Mono for headings/buttons (italic), duotone filter (red→light red), root padding 0.

### 3. Canary

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#fdff85` (bright yellow) |
| Contrast | `contrast` | `#000000` |
| Primary | `primary` | `#000000` |
| Secondary | `secondary` | `#353535` |
| Tertiary | `tertiary` | `#ffffff` |

**Key changes:** Full monospace theme (IBM Plex Mono body), font size small (0.75rem), wide size → 650px, images with top-left rounded corner (100px), buttons 5px radius with 2px border, duotone default (black→white).

### 4. Electric

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#f3f3f1` (off-white) |
| Contrast | `contrast` | `#2500ff` (electric blue) |
| Primary | `primary` | `#f3f3f1` |
| Secondary | `secondary` | `#2500ff` |
| Tertiary | `tertiary` | `#f6f6f6` |

**Key changes:** DM Sans body font, buttons with 2px border and custom padding, dotted underline on active/focus states.

### 5. Grapes

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#E1E1C7` (light beige) |
| Contrast | `contrast` | `#000000` |
| Primary | `primary` | `#214F31` (dark green) |
| Secondary | `secondary` | `#000000` |
| Tertiary | `tertiary` | `#F0EBD2` (cream) |

**Key changes:** Rounded buttons (9999px) with primary bg, Source Serif Pro for headings (600 weight), italic post date/terms, site title lowercase, dashed underline on link hover.

### 6. Marigold

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#F6F2EC` (beige) |
| Contrast | `contrast` | `#21251F` (dark brown) |
| Primary | `primary` | `#5B4460` (purple-brown) |
| Secondary | `secondary` | `#FCC263` (yellow) |
| Tertiary | `tertiary` | `#E7A1A9` (mauve) |

**Key changes:** Source Serif Pro body font, italic headings, pill buttons (50px radius) with secondary bg, custom spacing scale (6 sizes), extended font sizes with "tiny", "normal", "huge", "gigantic" slugs (9 total).

### 7. Pilgrimage

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#222828` (dark gray) |
| Contrast | `contrast` | `#ffffff` |
| Primary | `primary` | `#53ED85` (bright green) |
| Secondary | `secondary` | `#9EF9FD` (cyan) |
| Tertiary | `tertiary` | `#D8E202` (lime) |

**Key changes:** Dark theme with dots gradient background, navigation with primary color + underline, duotone filter (dark gray→cyan), buttons rounded (5px) with gradient (primary→secondary), H1/H2 contrast color, H3-H6 primary color, links primary with tertiary hover. 6 custom gradients.

### 8. Pitch

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#202124` (very dark gray) |
| Contrast | `contrast` | `#e8eaed` (light gray) |
| Primary | `primary` | `#e3cbc0` (tan) |
| Secondary | `secondary` | `#876C3A` (brown) |
| Tertiary | `tertiary` | `#303134` (dark gray) |

**Key changes:** Inter body font, content width → `min(640px, 90vw)`, wide width → `90vw`, buttons square (0 radius) + primary bg + uppercase, headings weight 500, custom 7-step spacing scale.

### 9. Sherbet

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#FFFFFF` |
| Contrast | `contrast` | `#000000` |
| Primary | `primary` | `#FFCCFF` (light magenta) |
| Secondary | `secondary` | `#FFFFCC` (light yellow) |
| Tertiary | `tertiary` | `#CCFFFF` (light cyan) |

**Key changes:** Navigation small + uppercase + weight 500, buttons rounded (99999px) + 2px border + gradient bg + uppercase, duotone filter (3-color: magenta, yellow, cyan), 3 custom gradients, x-small font size added (0.75rem).

### 10. Whisper

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#E5E7F2` (light purple-gray) |
| Contrast | `contrast` | `#47484B` (dark gray) |
| Primary | `primary` | `#B50B3E` (deep red) |
| Secondary | `secondary` | `#0B0033` (deep purple) |
| Tertiary | `tertiary` | `#F9F9FB` (nearly white) |

**Key changes:** Content width → 710px, navigation large + underline border, buttons rounded (10px) + transparent bg + primary border + shadow (2px 2px 6px), links with 2px solid underline border, quote/pullquote double borders (6px), tertiary root border with `max(1vw, 0.5rem)` width, custom fluid font sizes (H1–H6 with clamp() formulas).

---

## Button Styles

### Default Button

| Property | Value |
|----------|-------|
| Background | `var:preset|color|primary` (#9DFF20 — lime green) |
| Text | `var:preset|color|contrast` (#000000 — black) |
| Border Radius | 0 (sharp corners) |
| Hover | Background: `contrast`, text: `base` |
| Focus | Background: `contrast`, text: `base` |
| Active | Background: `secondary`, text: `base` |
| Visited | Text: `contrast` |

---

## Link Styles

| State | Color | Text Decoration |
|-------|-------|----------------|
| Default | `contrast` | underline |
| Hover | — | none |
| Focus | — | underline dashed |
| Active | `secondary` | none |

---

## Per-Block Default Styles (21 blocks configured)

### Navigation & Site

| Block | Key Styles |
|-------|-----------|
| `core/navigation` | Font size: small. Links: no underline; hover: underline; focus: underline dashed; active: none |
| `core/site-title` | Font size: medium, weight: normal, line-height: 1.4. Links: no underline; hover: underline; focus: dashed; active: secondary |

### Post Content

| Block | Key Styles |
|-------|-----------|
| `core/post-content` | Links color: `secondary` |
| `core/post-title` | Font size: inherit, weight: 400, margin: 1.25rem top/bottom. Links: no underline; hover: underline; focus: dashed; active: secondary + none |
| `core/post-author` | Font size: small |
| `core/post-date` | Font size: small, weight: 400. Links: no underline; hover: underline |
| `core/post-terms` | Font size: small |
| `core/post-excerpt` | Font size: medium |

### Comment Blocks

| Block | Key Styles |
|-------|-----------|
| `core/comments-title` | Font size: large, margin-bottom: spacing-40 |
| `core/comment-author-name` | Links: no underline; hover: underline; focus: dashed; active: secondary + none |
| `core/comment-date` | Font size: small. Links: no underline; hover: underline; focus: dashed; active: secondary + none |
| `core/comment-edit-link` | Font size: small |
| `core/comment-reply-link` | Font size: small |
| `core/comments-pagination` | Margin-top: spacing-40, link text-decoration: none |

### Content Blocks

| Block | Key Styles |
|-------|-----------|
| `core/pullquote` | Border: 1px solid top/bottom, line-height: 1.3, margin: spacing-40 top/bottom (important). Cite: small size, normal style, no text-transform |
| `core/quote` | Left border: 1px solid inherit, padding: spacing-30 left/right. Cite: small, normal style |
| `core/separator` | Non-full/wide: 100px width (CSS rule) |

### Query & Pagination

| Block | Key Styles |
|-------|-----------|
| `core/query` | Element h2: x-large font size |
| `core/query-pagination` | Font size: small, weight: 400. Links: no underline; hover: underline |
