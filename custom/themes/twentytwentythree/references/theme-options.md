# Twenty Twenty-Three — Configurable Options

All values below are the **theme.json defaults**. User overrides are stored in Global Styles (`wp_global_styles` post type). Use `var:preset|{type}|{slug}` format to reference presets in styles.

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

**Notes:** No default duotone or gradient presets. 5-color palette is intentionally minimal to encourage style variations.

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

| Name | Slug | Font Stack | Weight Range | Type |
|------|------|-----------|-------------|------|
| DM Sans | `dm-sans` | `"DM Sans", sans-serif` | 400, 700 (with italic) | Sans-serif |
| IBM Plex Mono | `ibm-plex-mono` | `'IBM Plex Mono', monospace` | 300, 400, 700 (with italic) | Monospace |
| Inter | `inter` | `"Inter", sans-serif` | 200–900 (variable) | Sans-serif |
| System Font | `system-font` | System stack | — | Fallback |
| Source Serif Pro | `source-serif-pro` | `"Source Serif Pro", serif` | 200–900 (variable, with italic) | Serif |

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

### Template Parts

| Title | Slug | Area |
|-------|------|------|
| Header | `header` | header |
| Footer | `footer` | footer |
| Comments Template Part | `comments` | uncategorized |
| Post Meta | `post-meta` | uncategorized |

---

## Style Variations

Twenty Twenty-Three includes **10 style variations** in its `styles/` directory. Each variation redefines colors, fonts, and element styles. They can be applied via the Site Editor or programmatically (see SKILL.md procedure step 3).

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

---

## Link Styles

| State | Color | Text Decoration |
|-------|-------|----------------|
| Default | `contrast` | underline |
| Hover | — | none |
| Focus | — | underline dashed |
| Active | `secondary` | none |

---

## Per-Block Default Styles

### core/navigation
- Font size: small
- Links: no underline; hover: underline; focus: underline dashed; active: none

### core/post-content
- Links color: `secondary`

### core/post-title
- Margin: 1.25rem top/bottom, weight: 400
- Links: no underline; hover: underline; focus: dashed; active: `secondary` + none

### core/post-date
- Font size: small, weight: 400
- Links: no underline; hover: underline

### core/post-terms
- Font size: small

### core/post-excerpt
- Font size: medium

### core/comments-title
- Font size: large
- Margin bottom: `spacing-40`

### core/pullquote
- Border: 1px solid top/bottom
- Cite: small size, normal style, no text-transform
- Line height: 1.3
- Margin: `spacing-40` top/bottom

### core/quote
- Left border: 1px solid inherit
- Padding: `spacing-30` left/right
- Cite: small, normal style

### core/query-pagination
- Font size: small, weight: 400
- Links: no underline; hover: underline

### core/site-title
- Font size: medium, weight: normal, line-height: 1.4
- Links: no underline; hover: underline; focus: dashed; active: `secondary`

### core/separator
- Non-full/wide: 100px width

### core/post-author
- Font size: small
