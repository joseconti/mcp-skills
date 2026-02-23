# Twenty Twenty-Four — Configurable Options

All values below are the **theme.json defaults**. User overrides are stored in Global Styles (`wp_global_styles` post type). Use `var:preset|{type}|{slug}` format to reference presets in styles.

---

## Color Palette

| Name | Slug | Default | CSS Variable |
|------|------|---------|-------------|
| Base | `base` | `#f9f9f9` | `--wp--preset--color--base` |
| Base / Two | `base-2` | `#ffffff` | `--wp--preset--color--base-2` |
| Contrast | `contrast` | `#111111` | `--wp--preset--color--contrast` |
| Contrast / Two | `contrast-2` | `#636363` | `--wp--preset--color--contrast-2` |
| Contrast / Three | `contrast-3` | `#A4A4A4` | `--wp--preset--color--contrast-3` |
| Accent | `accent` | `#cfcabe` | `--wp--preset--color--accent` |
| Accent / Two | `accent-2` | `#c2a990` | `--wp--preset--color--accent-2` |
| Accent / Three | `accent-3` | `#d8613c` | `--wp--preset--color--accent-3` |
| Accent / Four | `accent-4` | `#b1c5a4` | `--wp--preset--color--accent-4` |
| Accent / Five | `accent-5` | `#b5bdbc` | `--wp--preset--color--accent-5` |

**Default styles:** Background = `base`, Text = `contrast`

### To change a color

```json
mcm/set-global-styles {
  "settings": {
    "color": {
      "palette": {
        "theme": [
          {"color": "#f9f9f9", "name": "Base", "slug": "base"},
          {"color": "#ffffff", "name": "Base / Two", "slug": "base-2"},
          {"color": "#111111", "name": "Contrast", "slug": "contrast"},
          {"color": "#636363", "name": "Contrast / Two", "slug": "contrast-2"},
          {"color": "#A4A4A4", "name": "Contrast / Three", "slug": "contrast-3"},
          {"color": "#cfcabe", "name": "Accent", "slug": "accent"},
          {"color": "#c2a990", "name": "Accent / Two", "slug": "accent-2"},
          {"color": "#d8613c", "name": "Accent / Three", "slug": "accent-3"},
          {"color": "#b1c5a4", "name": "Accent / Four", "slug": "accent-4"},
          {"color": "#b5bdbc", "name": "Accent / Five", "slug": "accent-5"}
        ]
      }
    }
  }
}
```

---

## Duotone Presets

| Name | Slug | Colors |
|------|------|--------|
| Black and white | `duotone-1` | `#111111`, `#ffffff` |
| Black and sandstone | `duotone-2` | `#111111`, `#C2A990` |
| Black and rust | `duotone-3` | `#111111`, `#D8613C` |
| Black and sage | `duotone-4` | `#111111`, `#B1C5A4` |
| Black and pastel blue | `duotone-5` | `#111111`, `#B5BDBC` |

**Usage in block attributes:** `"style":{"color":{"duotone":"var:preset|duotone|duotone-1"}}`

---

## Gradient Presets

### Soft Gradients

| Name | Slug | Value |
|------|------|-------|
| Vertical soft beige to white | `gradient-1` | `linear-gradient(to bottom, #cfcabe 0%, #F9F9F9 100%)` |
| Vertical soft sandstone to white | `gradient-2` | `linear-gradient(to bottom, #C2A990 0%, #F9F9F9 100%)` |
| Vertical soft rust to white | `gradient-3` | `linear-gradient(to bottom, #D8613C 0%, #F9F9F9 100%)` |
| Vertical soft sage to white | `gradient-4` | `linear-gradient(to bottom, #B1C5A4 0%, #F9F9F9 100%)` |
| Vertical soft mint to white | `gradient-5` | `linear-gradient(to bottom, #B5BDBC 0%, #F9F9F9 100%)` |
| Vertical soft pewter to white | `gradient-6` | `linear-gradient(to bottom, #A4A4A4 0%, #F9F9F9 100%)` |

### Hard Gradients

| Name | Slug | Value |
|------|------|-------|
| Vertical hard beige to white | `gradient-7` | `linear-gradient(to bottom, #cfcabe 50%, #F9F9F9 50%)` |
| Vertical hard sandstone to white | `gradient-8` | `linear-gradient(to bottom, #C2A990 50%, #F9F9F9 50%)` |
| Vertical hard rust to white | `gradient-9` | `linear-gradient(to bottom, #D8613C 50%, #F9F9F9 50%)` |
| Vertical hard sage to white | `gradient-10` | `linear-gradient(to bottom, #B1C5A4 50%, #F9F9F9 50%)` |
| Vertical hard mint to white | `gradient-11` | `linear-gradient(to bottom, #B5BDBC 50%, #F9F9F9 50%)` |
| Vertical hard pewter to white | `gradient-12` | `linear-gradient(to bottom, #A4A4A4 50%, #F9F9F9 50%)` |

---

## Typography

### Font Families

| Name | Slug | Font Stack | Weight Range | Type |
|------|------|-----------|-------------|------|
| Inter | `body` | `"Inter", sans-serif` | 300–900 (variable) | Body text |
| Cardo | `heading` | `Cardo` | 400, 700 | Headings |
| System Sans-serif | `system-sans-serif` | System stack | — | Fallback |
| System Serif | `system-serif` | Iowan Old Style, etc. | — | Fallback |

**Default body font:** `body` (Inter)
**Default heading font:** `heading` (Cardo)

### Font Sizes

| Name | Slug | Default Size | Fluid Min | Fluid Max | CSS Variable |
|------|------|-------------|-----------|-----------|-------------|
| Small | `small` | `0.9rem` | — (fixed) | — | `--wp--preset--font-size--small` |
| Medium | `medium` | `1.05rem` | — (fixed) | — | `--wp--preset--font-size--medium` |
| Large | `large` | `1.85rem` | `1.39rem` | `1.85rem` | `--wp--preset--font-size--large` |
| Extra Large | `x-large` | `2.5rem` | `1.85rem` | `2.5rem` | `--wp--preset--font-size--x-large` |
| Extra Extra Large | `xx-large` | `3.27rem` | `2.5rem` | `3.27rem` | `--wp--preset--font-size--xx-large` |

### Default Body Typography

| Property | Value | Reference |
|----------|-------|-----------|
| Font Family | Inter | `var:preset|font-family|body` |
| Font Size | Medium | `var:preset|font-size|medium` |
| Font Style | normal | — |
| Font Weight | 400 | — |
| Line Height | 1.55 | — |

### Heading Typography

| Property | Value |
|----------|-------|
| Font Family | `var:preset|font-family|heading` (Cardo) |
| Font Weight | 400 |
| Line Height | 1.2 |

| Heading | Font Size |
|---------|-----------|
| H1 | `var:preset|font-size|xx-large` (line-height: 1.15) |
| H2 | `var:preset|font-size|x-large` |
| H3 | `var:preset|font-size|large` |
| H4 | `clamp(1.1rem, 1.1rem + ((1vw - 0.2rem) * 0.767), 1.5rem)` |
| H5 | `var:preset|font-size|medium` |
| H6 | `var:preset|font-size|small` |

---

## Layout

| Property | Value |
|----------|-------|
| Content Size | 620px |
| Wide Size | 1280px |

---

## Spacing

### Spacing Scale

| Name | Slug | Default Size | CSS Variable |
|------|------|-------------|-------------|
| 1 | `10` | `1rem` | `--wp--preset--spacing--10` |
| 2 | `20` | `min(1.5rem, 2vw)` | `--wp--preset--spacing--20` |
| 3 | `30` | `min(2.5rem, 3vw)` | `--wp--preset--spacing--30` |
| 4 | `40` | `min(4rem, 5vw)` | `--wp--preset--spacing--40` |
| 5 | `50` | `min(6.5rem, 8vw)` | `--wp--preset--spacing--50` |
| 6 | `60` | `min(10.5rem, 13vw)` | `--wp--preset--spacing--60` |

**Default spacing:**
- Block Gap: `1.2rem`
- Root Padding (left/right): `var:preset|spacing|50`

**Allowed units:** `%`, `px`, `em`, `rem`, `vh`, `vw`

---

## Templates & Template Parts

### Custom Templates

| Title | Slug | Post Types |
|-------|------|-----------|
| Page No Title | `page-no-title` | page |
| Page with Sidebar | `page-with-sidebar` | page |
| Page with Wide Image | `page-wide` | page |
| Single with Sidebar | `single-with-sidebar` | post |

### Template Parts

| Title | Slug | Area |
|-------|------|------|
| Header | `header` | header |
| Footer | `footer` | footer |
| Sidebar | `sidebar` | uncategorized |
| Post Meta | `post-meta` | uncategorized |

---

## Block Patterns (from pattern directory)

- `three-columns-of-services`
- `clients-section`

---

## Button Styles

### Default Button

| Property | Value |
|----------|-------|
| Background | `var:preset|color|contrast` |
| Text | `var:preset|color|base` |
| Border | `0.33rem` radius, `contrast` color |
| Font Size | `var:preset|font-size|small` |
| Font Weight | 500 |
| Padding | `0.6rem 1rem` |
| Hover | Background: `contrast-2`, text: `base` |
| Focus | Background: `contrast-2`, outline: `contrast` (2px offset) |
| Active | Background: `contrast`, text: `base` |

### Outline Variation

| Property | Value |
|----------|-------|
| Border Width | 1px |
| Padding | `calc(0.6rem - 1px) calc(1rem - 1px)` |

---

## Link Styles

| State | Color | Text Decoration |
|-------|-------|----------------|
| Default | `contrast` | inherited |
| Hover | — | none |

---

## Per-Block Default Styles

### core/code
- Border: `contrast`, radius: `spacing-20`
- Background: `base-2`, text: `contrast-2`
- Font: medium size, normal style, weight 400, line-height 1.6
- Padding: `calc(spacing-30 + 0.75rem)` all sides

### core/quote
- Background: `base-2`, border-radius: `spacing-20`
- Font: `heading` family, large size, italic, line-height 1.3
- **Plain variation:** transparent background, no border, `body` family, medium size, normal style

### core/pullquote
- Font: `heading` family, `x-large` size, italic, weight 400, line-height 1.5
- Border radius: `spacing-20`
- Padding: `spacing-40` top/bottom

### core/navigation
- Links: no underline, underline on hover
- Font weight: 500

### core/search
- Input: 0.33rem border-radius
- Button: inherits button border-radius

### core/separator
- 1px solid bottom border, color: `contrast`
- Non-full-width default: `spacing-60` max-width

### core/image
- **Rounded variation:** border-radius: `spacing-20`

### core/site-title
- Font: `body` family, 1.2rem size, weight 600, normal style
- Link: no underline (no change on hover)

### core/post-date
- Color: `contrast-2`, font size: small
- Link: `contrast-2`, no underline, underline on hover

### core/post-featured-image
- Border radius: `spacing-20`

### core/avatar
- Border radius: 90px
