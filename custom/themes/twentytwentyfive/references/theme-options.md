# Twenty Twenty-Five — Configurable Options

All values below are the **theme.json defaults**. User overrides are stored in Global Styles (`wp_global_styles` post type). Use `var:preset|{type}|{slug}` format to reference presets in styles.

---

## Color Palette

| Name | Slug | Default | CSS Variable |
|------|------|---------|-------------|
| Base | `base` | `#FFFFFF` | `--wp--preset--color--base` |
| Contrast | `contrast` | `#111111` | `--wp--preset--color--contrast` |
| Accent 1 | `accent-1` | `#FFEE58` | `--wp--preset--color--accent-1` |
| Accent 2 | `accent-2` | `#F6CFF4` | `--wp--preset--color--accent-2` |
| Accent 3 | `accent-3` | `#503AA8` | `--wp--preset--color--accent-3` |
| Accent 4 | `accent-4` | `#686868` | `--wp--preset--color--accent-4` |
| Accent 5 | `accent-5` | `#FBFAF3` | `--wp--preset--color--accent-5` |
| Accent 6 | `accent-6` | `color-mix(in srgb, currentColor 20%, transparent)` | `--wp--preset--color--accent-6` |

**Default styles:** Background = `base`, Text = `contrast`

**Notes:** No default duotone, gradients, or core palette (all disabled). Accent 6 is dynamic (20% of current text color).

### To change a color

```json
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
```

---

## Typography

### Font Families

| Name | Slug | Font Stack | Weight Range |
|------|------|-----------|-------------|
| Manrope | `manrope` | `Manrope, sans-serif` | 200–800 (variable) |
| Fira Code | `fira-code` | `"Fira Code", monospace` | 300–700 (variable) |

**Default body font:** `manrope`

### Font Sizes

| Name | Slug | Default Size | Fluid Min | Fluid Max | CSS Variable |
|------|------|-------------|-----------|-----------|-------------|
| Small | `small` | `0.875rem` | — (fixed) | — | `--wp--preset--font-size--small` |
| Medium | `medium` | `1rem` | `1rem` | `1.125rem` | `--wp--preset--font-size--medium` |
| Large | `large` | `1.38rem` | `1.125rem` | `1.375rem` | `--wp--preset--font-size--large` |
| Extra Large | `x-large` | `1.75rem` | `1.75rem` | `2rem` | `--wp--preset--font-size--x-large` |
| Extra Extra Large | `xx-large` | `2.15rem` | `2.15rem` | `3rem` | `--wp--preset--font-size--xx-large` |

### Default Body Typography

| Property | Value | Reference |
|----------|-------|-----------|
| Font Family | Manrope | `var:preset|font-family|manrope` |
| Font Size | Large | `var:preset|font-size|large` |
| Font Weight | 300 | — |
| Letter Spacing | -0.1px | — |
| Line Height | 1.4 | — |

### Heading Typography

| Property | Value |
|----------|-------|
| Font Weight | 400 |
| Line Height | 1.125 |
| Letter Spacing | -0.1px |

| Heading | Font Size |
|---------|-----------|
| H1 | `var:preset|font-size|xx-large` |
| H2 | `var:preset|font-size|x-large` |
| H3 | `var:preset|font-size|large` |
| H4 | `var:preset|font-size|medium` |
| H5 | `var:preset|font-size|small` (letter-spacing: 0.5px) |
| H6 | `var:preset|font-size|small` (weight: 700, letter-spacing: 1.4px, uppercase) |

### To change body typography

```json
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
```

---

## Layout

| Property | Value |
|----------|-------|
| Content Size | 645px |
| Wide Size | 1340px |

### To change layout

```json
mcm/set-global-styles {
  "settings": {
    "layout": {
      "contentSize": "720px",
      "wideSize": "1200px"
    }
  }
}
```

---

## Spacing

### Spacing Scale

| Name | Slug | Default Size | CSS Variable |
|------|------|-------------|-------------|
| Tiny | `20` | `10px` | `--wp--preset--spacing--20` |
| X-Small | `30` | `20px` | `--wp--preset--spacing--30` |
| Small | `40` | `30px` | `--wp--preset--spacing--40` |
| Regular | `50` | `clamp(30px, 5vw, 50px)` | `--wp--preset--spacing--50` |
| Large | `60` | `clamp(30px, 7vw, 70px)` | `--wp--preset--spacing--60` |
| X-Large | `70` | `clamp(50px, 7vw, 90px)` | `--wp--preset--spacing--70` |
| XX-Large | `80` | `clamp(70px, 10vw, 140px)` | `--wp--preset--spacing--80` |

**Default spacing:**
- Block Gap: `1.2rem`
- Root Padding (left/right): `var:preset|spacing|50`

**Allowed units:** `%`, `px`, `em`, `rem`, `vh`, `vw`

---

## Templates & Template Parts

### Custom Templates

| Name | Slug | Post Types |
|------|------|-----------|
| Page No Title | `page-no-title` | page |

### Template Parts

| Title | Slug | Area |
|-------|------|------|
| Header | `header` | header |
| Vertical site header | `vertical-header` | header |
| Header with large title | `header-large-title` | header |
| Footer | `footer` | footer |
| Footer Columns | `footer-columns` | footer |
| Footer Newsletter | `footer-newsletter` | footer |
| Sidebar | `sidebar` | uncategorized |

---

## Post Formats

Supported: `aside`, `audio`, `chat`, `gallery`, `image`, `link`, `quote`, `status`, `video`

---

## Button Styles

### Default Button

| Property | Value |
|----------|-------|
| Background | `var:preset|color|contrast` |
| Text | `var:preset|color|base` |
| Font Size | `var:preset|font-size|medium` |
| Padding | `1rem 2.25rem` |
| Hover Background | `color-mix(in srgb, var(--wp--preset--color--contrast) 85%, transparent)` |

### Outline Variation

| Property | Value |
|----------|-------|
| Border | `1px solid currentColor` |
| Padding | `calc(1rem - 1px) calc(2.25rem - 1px)` |

---

## Link Styles

| State | Color | Text Decoration |
|-------|-------|----------------|
| Default | `currentColor` | inherited |
| Hover | — | none |

---

## Per-Block Default Styles

### core/code
- Font: `fira-code`, medium size, weight 300
- Background: `accent-5`, text: `contrast`
- Padding: `spacing-40` all sides

### core/quote
- Left border: 2px solid currentColor
- Font size: large, weight 300
- Padding: `spacing-30` top/bottom, `spacing-40` left/right
- **Plain variation:** no border, no padding

### core/pullquote
- Font size: `xx-large`, weight 300, line-height 1.2
- Padding: `spacing-30` top/bottom

### core/navigation
- Font size: medium
- Links: no underline, underline on hover

### core/search
- Input: rounded (3.125rem border-radius)
- Button: rounded (3.125rem border-radius)

### core/separator
- 1px solid bottom border, color: `accent-6`

### core/avatar
- Border radius: 100px (circular)

### core/site-title
- Font weight: 700, letter-spacing: -0.5px
- Link: no underline, underline on hover

### core/post-date
- Color: `accent-4`, font size: small

### core/post-terms
- Font size: small, weight: 600
