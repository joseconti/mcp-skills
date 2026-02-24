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

**Body font:** DM Sans. **Background:** gradient `base→secondary→base` (vertical, clamp 10vh-14vh).

**Custom font sizes:** small 1rem (0.875→1), medium 1.125rem (1→1.125), large 1.75rem (fixed), x-large 3.25rem (fixed), xx-large 10rem (10→16.3).

**4 custom gradients:**
1. `secondary-base` — linear 180deg secondary→base
2. `base-secondary-base` — linear 180deg base 0 clamp(10vh,24rem,14vh) → secondary 30% → base 100%
3. `tertiary-primary` — linear 90deg tertiary 5.74% → primary 100%
4. `primary-tertiary` — linear 90deg primary 5.74% → tertiary 100%

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/comment-reply-link` | Link: primary color, italic |
| `core/group` | Border color: primary |
| `core/navigation` | fontSize: medium |
| `core/post-author` | Color: primary, italic |
| `core/post-content` | Link color: primary |
| `core/post-date` | Link: contrast color, letterSpacing 0.09rem, uppercase |
| `core/post-terms` | Link: primary color, italic |
| `core/post-title` | fontSize: clamp(2.625rem…3.25rem). Link :active = contrast |
| `core/query` | h3: primary, large, weight 700. Link: primary |
| `core/separator` | Color: primary |
| `core/site-title` | Border: primary 0 0 2px 0. Link :active/:focus/:hover = primary (no underline). letterSpacing 0.09rem, uppercase |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 99999px, gradient tertiary→primary, text = base. :hover/:focus/:active = primary bg (no gradient), text secondary. :visited = base |
| `heading` | letterSpacing: -0.019rem |
| `link` | :active = primary |

---

### 2. Block Out

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#ff5252` (bright red) |
| Contrast | `contrast` | `#252525` (dark gray) |
| Primary | `primary` | `#ffffff` |
| Secondary | `secondary` | `#ff2d34` (red) |
| Tertiary | `tertiary` | `#ff7e7e` (light red) |

**Body font:** DM Sans. **Layout:** contentSize 800px. **Root padding:** top/bottom 0px.

**Custom font sizes:** small 1rem (0.875→1), medium 1.125rem (1→1.125), large 1.75rem (fixed), x-large 2.25rem (fixed), xx-large 7rem (4.3→7).

**Custom duotone:** `default-filter` — #E2161D → #FF9C9C.

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/avatar` | Duotone: default-filter |
| `core/image` | Border radius 8px, duotone: default-filter |
| `core/navigation` | fontSize: large |
| `core/post-content` | Link color: contrast. h1 color: contrast |
| `core/post-featured-image` | Border radius 8px, duotone: default-filter |
| `core/post-title` | Color: primary. Link :active = primary |
| `core/query` | h2 fontSize: large |
| `core/quote` | Border width: 1px |
| `core/search` | Border radius 8px |
| `core/site-logo` | Duotone: default-filter |
| `core/site-title` | fontSize xx-large, lineHeight 1.1, lowercase. Padding top/bottom spacing-30. Link :active = primary |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 8px, fontFamily IBM Plex Mono, italic, weight 400. :active text = contrast |
| `h1` | Color: primary |
| `h6` | Weight: 400 |
| `heading` | fontFamily IBM Plex Mono, italic |
| `link` | fontFamily IBM Plex Mono, italic, weight 400. :active = primary |

---

### 3. Canary

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#fdff85` (bright yellow) |
| Contrast | `contrast` | `#000000` |
| Primary | `primary` | `#000000` |
| Secondary | `secondary` | `#353535` |
| Tertiary | `tertiary` | `#ffffff` |

**Body font:** IBM Plex Mono, fontSize small. **Layout:** wideSize 650px.

**Custom font sizes:** small 0.75rem, medium 1.125rem, large 1.75rem, x-large 2.25rem, xx-large 10rem (all fixed, no fluid).

**Custom duotone:** `default-filter` — #000000 → #ffffff.

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/comments` | Link: underline; :hover none |
| `core/comment-reply-link` | fontSize: small |
| `core/comments-title` | fontSize: small |
| `core/image` | Border radius 100px 0 0 0, duotone default-filter |
| `core/navigation` | lowercase |
| `core/post-content` | Link underline; :hover none |
| `core/post-excerpt` | fontSize: small |
| `core/post-featured-image` | Border radius 100px 0 0 0, margin/padding all 0 |
| `core/post-title` | Weight: 700 |
| `core/separator` | Border width: 2px |
| `core/site-title` | Weight 700, lowercase, fontSize small |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 5px, border 2px solid contrast, text base. Padding 0.667em 1.333em. :hover/:focus = base bg, contrast text, 2px border. :visited = base |
| `h1` | fontSize: small |
| `h2` | fontSize: small |
| `h3` | fontSize: small |
| `h4` | fontSize: small |
| `heading` | Weight: 700 |
| `link` | textDecoration: none |

---

### 4. Electric

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#f3f3f1` (off-white) |
| Contrast | `contrast` | `#2500ff` (electric blue) |
| Primary | `primary` | `#f3f3f1` |
| Secondary | `secondary` | `#2500ff` |
| Tertiary | `tertiary` | `#f6f6f6` |

**Body font:** DM Sans. No layout, font size, or spacing changes.

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Border 2px solid contrast, bg contrast, text base. Padding .667em 1.333em. :active/:focus = underline dotted. :hover = base bg, contrast text, 2px border. :visited = base |
| `link` | :focus/:active = underline dotted |

---

### 5. Grapes

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#E1E1C7` (light beige) |
| Contrast | `contrast` | `#000000` |
| Primary | `primary` | `#214F31` (dark green) |
| Secondary | `secondary` | `#000000` |
| Tertiary | `tertiary` | `#F0EBD2` (cream) |

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/post-comments` | Link :hover = underline dashed |
| `core/post-date` | fontFamily Source Serif Pro, italic |
| `core/post-terms` | fontFamily Source Serif Pro, italic |
| `core/site-title` | lowercase |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 9999px, bg primary, text base. :visited = base |
| `heading` | fontFamily Source Serif Pro, weight 600 |
| `link` | :hover = underline dashed |

---

### 6. Marigold

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#F6F2EC` (beige) |
| Contrast | `contrast` | `#21251F` (dark brown) |
| Primary | `primary` | `#5B4460` (purple-brown) |
| Secondary | `secondary` | `#FCC263` (yellow) |
| Tertiary | `tertiary` | `#E7A1A9` (mauve) |

**Body font:** Source Serif Pro, fontSize normal, lineHeight 1.5. **blockGap:** 2.5rem. **Root padding:** top/bottom spacing-50, left/right spacing-40.

**Custom font sizes (9 slugs):**

| Slug | Size |
|------|------|
| `tiny` | clamp(0.875rem, 0.799rem + 0.24vw, 1rem) |
| `small` | clamp(1rem, 0.924rem + 0.24vw, 1.125rem) |
| `normal` | clamp(1.125rem, 1.049rem + 0.24vw, 1.25rem) |
| `medium` | clamp(1.25rem, 1.021rem + 0.73vw, 1.625rem) |
| `large` | clamp(1.375rem, 1.07rem + 0.98vw, 1.875rem) |
| `x-large` | clamp(1.75rem, 1.369rem + 1.22vw, 2.375rem) |
| `xx-large` | clamp(2.125rem, 1.706rem + 1.34vw, 2.813rem) |
| `huge` | clamp(2.5rem, 1.966rem + 1.71vw, 3.375rem) |
| `gigantic` | clamp(3.375rem, 2.384rem + 3.17vw, 5rem) |

**Custom spacing scale (6 sizes):**

| Slug | Size |
|------|------|
| `30` | clamp(0.625rem, 0.434rem + 0.61vw, 0.938rem) |
| `40` | clamp(1.25rem, 0.869rem + 1.22vw, 1.875rem) |
| `50` | clamp(1.875rem, 1.303rem + 1.83vw, 2.813rem) |
| `60` | clamp(2.5rem, 1.738rem + 2.44vw, 3.75rem) |
| `70` | clamp(2.813rem, 1.098rem + 5.49vw, 5.625rem) |
| `80` | clamp(3.75rem, 1.463rem + 7.32vw, 7.5rem) |

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/comment-author-name` | Link :active = primary |
| `core/query` | Padding left/right = 0 |
| `core/post-content` | Link color: primary |
| `core/post-excerpt` | fontSize: normal |
| `core/post-title` | fontSize large, weight 600, margin top/bottom spacing-50. Link: primary color, no underline |
| `core/pullquote` | Border width 1px 0 |
| `core/query-pagination` | fontSize small, weight 400. Link: no underline |
| `core/quote` | fontSize 1.625rem, lineHeight 1.5. Cite: 1.25rem |
| `core/site-title` | fontSize normal, lowercase |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `h1` | fontSize huge, lineHeight 1.1 |
| `h2` | fontSize xx-large, lineHeight 1.2 |
| `h3` | fontSize x-large, lineHeight 1.2 |
| `h4` | fontSize large, weight 600 |
| `h5` | fontStyle normal, weight 600, textTransform none |
| `h6` | fontSize normal, fontStyle normal, weight 600 |
| `heading` | fontStyle italic |
| `link` | :active = primary. :hover = none (textDecoration) |
| `button` | Radius 50px, bg secondary, fontSize normal. :hover = tertiary bg, contrast text. :focus/:active = primary bg |

---

### 7. Pilgrimage

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#222828` (dark gray) |
| Contrast | `contrast` | `#ffffff` |
| Primary | `primary` | `#53ED85` (bright green) |
| Secondary | `secondary` | `#9EF9FD` (cyan) |
| Tertiary | `tertiary` | `#D8E202` (lime) |

**Background:** gradient `dots` (radial dot pattern + dark base). Dark theme.

**Custom duotone:** `default-filter` — #222828 → #9EF9FD.

**6 custom gradients:**
1. `primary-secondary` — linear 180deg primary→secondary
2. `secondary-primary` — linear 180deg secondary→primary
3. `tertiary-secondary` — linear 180deg primary→secondary (mislabeled)
4. `tertiary-primary` — linear 180deg tertiary→primary
5. `base-primary` — linear 180deg base→primary 350%
6. `dots` — radial-gradient(circle at 5px 5px, #0c0d0d70 2px, transparent 0) 0 0 / 8px 8px, linear 180deg base→#000 200%

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/comment-author-name` | Link :active = tertiary |
| `core/comment-date` | Link :active = tertiary + underline |
| `core/comment-edit-link` | Link :active = tertiary |
| `core/comments-pagination` | Link: underline |
| `core/image` | Duotone: default-filter |
| `core/navigation` | Link: primary color, underline. :active = underline dashed |
| `core/paragraph` | Color: contrast. Link :hover = tertiary |
| `core/post-content` | Link color: primary |
| `core/post-date` | Link: no underline, italic |
| `core/post-featured-image` | Duotone: default-filter |
| `core/post-title` | Link underline. :active = tertiary + underline |
| `core/query-pagination` | Link: underline |
| `core/separator` | Color: secondary |
| `core/site-title` | Italic, weight 700. Link :active = primary |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 5px, gradient primary→secondary, text base. :active = secondary bg (no gradient). :focus/:hover = gradient secondary→primary. :visited = base |
| `h1` | Color: contrast |
| `h2` | Color: contrast |
| `h3` | Color: primary |
| `h4` | Color: primary |
| `h5` | Color: primary |
| `h6` | Color: primary |
| `heading` | Color: primary |
| `link` | Color primary. :hover/:focus/:active = tertiary |

---

### 8. Pitch

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#202124` (very dark gray) |
| Contrast | `contrast` | `#e8eaed` (light gray) |
| Primary | `primary` | `#e3cbc0` (tan) |
| Secondary | `secondary` | `#876C3A` (brown) |
| Tertiary | `tertiary` | `#303134` (dark gray) |

**Body font:** Inter, fontSize medium, lineHeight 1.7. **Layout:** contentSize min(640px, 90vw), wideSize 90vw. **blockGap:** spacing-40. **Root padding:** left/right spacing-70.

**Custom font sizes:**

| Slug | Size | Fluid |
|------|------|-------|
| `small` | 0.85rem | 0.85→1rem |
| `medium` | 1.1rem | 1.1→1.4rem |
| `large` | 1.999rem | 1.999→2.827rem |
| `x-large` | 2.827rem | 2.827→3.998rem |
| `xx-large` | 3.2rem | 3.2→5.2rem |

**Custom spacing scale (7 sizes):**

| Slug | Size |
|------|------|
| `20` | calc(8px + 1.5625vw) |
| `30` | calc(12px + 1.5625vw) |
| `40` | calc(16px + 1.5625vw) |
| `50` | calc(20px + 1.5625vw) |
| `60` | calc(24px + 1.5625vw) |
| `70` | calc(28px + 1.5625vw) |
| `80` | calc(32px + 1.5625vw) |

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/separator` | Border: tertiary, 2px |
| `core/site-title` | fontSize medium, fontStyle normal, weight 600 |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 0, border 2px solid primary, bg primary, text base. Padding min(1.125rem,3vw) min(2.125rem,5vw) !important. fontSize small, weight 600, uppercase, letterSpacing 0.01em. :hover/:focus/:active = border contrast, bg contrast, text tertiary. :visited = base |
| `h1` | fontSize xx-large, lineHeight 1.1 |
| `h2` | fontSize x-large, lineHeight 1.1 |
| `h3` | fontSize large |
| `heading` | Weight: 500 |

---

### 9. Sherbet

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#FFFFFF` |
| Contrast | `contrast` | `#000000` |
| Primary | `primary` | `#FFCCFF` (light magenta) |
| Secondary | `secondary` | `#FFFFCC` (light yellow) |
| Tertiary | `tertiary` | `#CCFFFF` (light cyan) |

**Body font:** Inter, fontSize small. **Background:** gradient primary→secondary→tertiary.

**Custom font sizes:** x-small 0.75rem (fixed), small 1rem (0.875→1), medium 1.125rem (1→1.125), large 1.75rem (1.5→1.75), x-large 2.25rem (2→2.25), xx-large 2.75rem (2.5→2.75).

**Custom duotone:** `default-filter` — 3 colors: #FF99FF, #FFFF99, #99FFFF.

**3 custom gradients:**
1. `primary-secondary-tertiary` — linear 135deg primary→secondary 50%→tertiary
2. `primary-secondary-tertiary-fixed` — same + `fixed`
3. `tertiary-secondary-primary-fixed` — linear 135deg tertiary→secondary 50%→primary + `fixed`

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/comments` | Link :active = contrast |
| `core/comment-author-name` | fontSize medium, textTransform initial |
| `core/comment-content` | fontSize medium, textTransform initial |
| `core/navigation` | fontSize small, weight 500, uppercase |
| `core/post-content` | Link: contrast. :active = contrast |
| `core/post-date` | Uppercase |
| `core/post-featured-image` | Duotone default-filter. Border: tertiary, solid |
| `core/post-title` | Weight 500, uppercase |
| `core/site-title` | Weight 500 |
| `core/template-part` | fontSize x-small, weight 400, uppercase |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 99999px, border 2px solid contrast. bg base, gradient primary-secondary-tertiary-fixed, text contrast. fontSize x-small, weight 400, uppercase. :hover = gradient tertiary-secondary-primary-fixed. :focus/:active = contrast bg, no gradient |
| `heading` | Weight: 500 |

---

### 10. Whisper

| Color | Slug | Hex |
|-------|------|-----|
| Base | `base` | `#E5E7F2` (light purple-gray) |
| Contrast | `contrast` | `#47484B` (dark gray) |
| Primary | `primary` | `#B50B3E` (deep red) |
| Secondary | `secondary` | `#0B0033` (deep purple) |
| Tertiary | `tertiary` | `#F9F9FB` (nearly white) |

**Body font:** DM Sans. **Layout:** contentSize 710px, wideSize 1200px. **Root border:** tertiary, solid, width max(1vw, 0.5rem). **Root padding:** top/bottom spacing-40, left/right spacing-30.

**Custom font sizes:** small 1rem (0.875→1), medium 1.187rem (1→1.187), large 1.3125rem (1.187→1.3125), x-large 2rem (1.562→2), xx-large 5.7rem (3.5→5.7).

**Per-block overrides:**

| Block | Changes |
|-------|---------|
| `core/image` | Link: border 0. :hover bg transparent |
| `core/navigation` | Color contrast. Link: border-bottom transparent 0.2ch, contrast color, no underline. :hover = border primary, bg transparent, text secondary. :focus/:active = no underline. fontSize large |
| `core/navigation-submenu` | Color: primary |
| `core/post-content` | Link :hover = border contrast, bg tertiary, no underline |
| `core/post-date` | Link :hover = border contrast, bg tertiary, no underline |
| `core/post-featured-image` | Link: border 0. :hover bg transparent |
| `core/post-title` | Link: border 0 !important. :hover/:focus/:active text = primary |
| `core/pullquote` | Border: contrast, double, 6px. Color: secondary |
| `core/quote` | Border: contrast, double, 0 0 0 6px. Color: secondary. margin-left spacing-30, padding-left spacing-30 |
| `core/query-pagination` | Link :hover = border contrast, bg tertiary, no underline. :active = border base 0 0 2px 0 |
| `core/separator` | Border: contrast, double, 6px 0 0 0 |
| `core/site-logo` | Link: border 0 |
| `core/site-title` | DM Sans, fontSize large, weight 700, letterSpacing -0.01em, lineHeight 1.4, capitalize. Link: border transparent, primary color, no underline. :hover = border primary, bg transparent. :focus/:active = no underline, border primary, bg transparent |
| `core/comment-author-name` | Link :hover/:focus = no underline |
| `core/comment-date` | Link :hover/:focus = no underline |
| `core/comment-edit-link` | Link :hover/:focus = no underline |

**Per-element overrides:**

| Element | Changes |
|---------|---------|
| `button` | Radius 10px, border primary 2px 2px 6px 2px solid !important, bg transparent, text primary. Padding min(1rem,3vw) min(2.75rem,6vw) !important. Weight 700, letterSpacing 1px, uppercase. :hover = border secondary 2px 2px 4px 2px, bg tertiary, text secondary, padding-bottom min(calc(1rem+2px),3vw). :focus = same + dashed dashed double border-style. :active = same as hover. :visited = primary |
| `cite` | fontFamily Source Serif Pro |
| `h1` | fontSize clamp(4.21rem, 1.43vw + 3.85rem, 5rem), weight 300, letterSpacing -0.01em |
| `h2` | Color secondary, fontSize clamp(3.16rem, 1.08vw + 2.89rem, 3.75rem), weight 400, letterSpacing -0.01em |
| `h3` | Color secondary, fontSize clamp(2.37rem, 0.81vw + 2.17rem, 2.81rem), weight 500 |
| `h4` | fontSize clamp(1.78rem, 0.61vw + 1.63rem, 2.11rem), weight 600 |
| `h5` | fontSize clamp(1.33rem, 0.45vw + 1.22rem, 1.58rem), weight 700, letterSpacing 1px |
| `h6` | fontSize clamp(1rem, 0.34vw + 0.91rem, 1.19rem), weight 900, letterSpacing 2px |
| `heading` | Color secondary, fontFamily Source Serif Pro |
| `link` | Border: primary solid 0 0 2px 0, color secondary. :hover = border contrast, text secondary, no underline. :focus = border dashed, no underline. :active = border 0, text secondary, no underline |

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
