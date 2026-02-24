# Twenty Twenty-Four — Complete Configurable Options

All values below are the **theme.json defaults**. User overrides are stored in Global Styles (`wp_global_styles` post type). Use `var:preset|{type}|{slug}` format to reference presets in styles.

---

## Global Settings

| Setting | Value | Description |
|---------|-------|-------------|
| `appearanceTools` | `true` | Enables all appearance editing tools |
| `useRootPaddingAwareAlignments` | `true` | Full-width blocks honor root padding |
| `typography.fluid` | `true` | Responsive fluid typography enabled |
| `typography.writingMode` | `true` | RTL language support |
| `color.defaultDuotone` | `false` | Only custom duotones |
| `color.defaultPalette` | `false` | Only custom palette |
| `color.defaultGradients` | `false` | Only custom gradients |
| `spacing.spacingScale.steps` | `0` | Custom spacing scale |
| `spacing.units` | `%`, `px`, `em`, `rem`, `vh`, `vw` | Allowed CSS units |

---

## Color Palette (10 colors)

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

## Duotone Presets (5)

| Name | Slug | Colors |
|------|------|--------|
| Black and white | `duotone-1` | `#111111`, `#ffffff` |
| Black and sandstone | `duotone-2` | `#111111`, `#C2A990` |
| Black and rust | `duotone-3` | `#111111`, `#D8613C` |
| Black and sage | `duotone-4` | `#111111`, `#B1C5A4` |
| Black and pastel blue | `duotone-5` | `#111111`, `#B5BDBC` |

**Usage in block attributes:** `"style":{"color":{"duotone":"var:preset|duotone|duotone-1"}}`

---

## Gradient Presets (12)

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
| Cardo | `heading` | `Cardo` | 400, 700 (with 400 italic) | Headings |
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

| Heading | Font Size | Additional |
|---------|-----------|------------|
| H1 | `var:preset|font-size|xx-large` | line-height: 1.15 |
| H2 | `var:preset|font-size|x-large` | — |
| H3 | `var:preset|font-size|large` | — |
| H4 | `clamp(1.1rem, 1.1rem + ((1vw - 0.2rem) * 0.767), 1.5rem)` | — |
| H5 | `var:preset|font-size|medium` | — |
| H6 | `var:preset|font-size|small` | — |

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

| Title | Slug | Post Types | Description |
|-------|------|-----------|-------------|
| Page No Title | `page-no-title` | page | Page without title |
| Page with Sidebar | `page-with-sidebar` | page | 3-column: content (60%) + sidebar (30%) |
| Page with Wide Image | `page-wide` | page | Hero layout with featured image |
| Single with Sidebar | `single-with-sidebar` | post | Post with sidebar |

### Default Templates

| File | Purpose | Key Content |
|------|---------|-------------|
| `page.html` | Single page | Header + title + featured image + content + footer |
| `single.html` | Single post | Title (centered, x-large) + featured image + content + tags + separator + comments + nav |
| `home.html` | Homepage | Embeds `page-home-business` pattern |
| `index.html` | Blog listing | Embeds `hidden-posts-heading` + `posts-3-col` patterns |
| `archive.html` | Archive page | Query title + `posts-3-col` pattern |
| `search.html` | Search results | Query title + search form + `posts-3-col` pattern |
| `404.html` | Error page | Embeds `hidden-404` pattern |

### Template Parts

| Title | Slug | Area | Content |
|-------|------|------|---------|
| Header | `header` | header | Logo + site title + navigation (flex, space-between) |
| Footer | `footer` | footer | References `twentytwentyfour/footer` pattern (4-col nav + colophon) |
| Sidebar | `sidebar` | uncategorized | References `twentytwentyfour/hidden-sidebar` pattern |
| Post Meta | `post-meta` | uncategorized | References `twentytwentyfour/hidden-post-meta` pattern |

---

## Custom Block Styles (from functions.php)

| Block | Style Name | Description |
|-------|-----------|-------------|
| `core/details` | `arrow-icon-details` | Arrow unicode characters (down/right) as list markers, changes on open |
| `core/post-terms` | `pill` | Inline pill/badge styling with background, padding, rounded corners |
| `core/list` | `checkmark-list` | Checkmark (✓) as list marker |
| `core/navigation-link` | `arrow-link` | Appends northeast arrow (↗) to link text |
| `core/heading` | `asterisk` | Decorative asterisk mark using SVG clip-path, responsive positioning |

---

## Block Patterns (57 total)

### Page Layout Patterns

| Slug | Description |
|------|-------------|
| `page-home-business` | Business home page (used by home.html) |
| `page-home-portfolio` | Portfolio home page |
| `page-portfolio-overview` | Portfolio overview page |
| `page-rsvp-landing` | RSVP/event landing page |
| `page-about-business` | About page for business |
| `page-home-blogging` | Blog-focused home page |

### Banner/Hero Patterns

| Slug | Description |
|------|-------------|
| `banner-hero` | Full-width hero with heading, paragraph, CTA button |
| `banner-hero-full` | Full-width hero (expanded) |
| `banner-project-description` | Project description banner |

### Call to Action Patterns

| Slug | Description |
|------|-------------|
| `cta-subscribe-centered` | Centered subscription CTA |
| `cta-services-image-left` | Services CTA with left image |
| `cta-content-image-on-right` | Content with image on right |
| `cta-rsvp` | RSVP form CTA |

### Gallery Patterns

| Slug | Description |
|------|-------------|
| `gallery-full-screen-image` | Full-screen image gallery |
| `gallery-project-layout` | Project gallery layout |
| `gallery-offset-images-grid-4-col` | 4-column offset grid |

### Post/Content Patterns

| Slug | Description |
|------|-------------|
| `posts-3-col` | 3-column query loop with featured image, title, meta, excerpt |
| `posts-images-only-3-col` | Image-only 3-column grid |
| `posts-images-only-offset-4-col` | Offset 4-column image grid |
| `text-feature-grid-3-col` | 3-column feature text grid |

### Template Patterns (9, used in default templates)

| Slug | Used By |
|------|---------|
| `template-home-blogging` | Blog-style home |
| `template-home-business` | Business home |
| `template-home-portfolio` | Portfolio home |
| `template-index-blogging` | Blog index |
| `template-index-portfolio` | Portfolio index |
| `template-archive-blogging` | Blog archive |
| `template-archive-portfolio` | Portfolio archive |
| `template-search-blogging` | Blog search |
| `template-search-portfolio` | Portfolio search |
| `template-single-portfolio` | Single portfolio item |

### Hidden Patterns (10, not in inserter)

| Slug | Purpose |
|------|---------|
| `hidden-404` | 404 error page content |
| `hidden-comments` | Comments section with threading and pagination |
| `hidden-no-results` | No results message + search form |
| `hidden-post-navigation` | Previous/next post navigation |
| `hidden-post-meta` | Post metadata display |
| `hidden-search` | Search heading |
| `hidden-sidebar` | Sidebar widget area |
| `hidden-portfolio-hero` | Portfolio hero section |

### Other Notable Patterns

| Slug | Description |
|------|-------------|
| `team-4-col` | 4-column team member grid |
| `testimonial-centered` | Centered testimonial |
| `footer` | 4-column footer with nav links and colophon |
| `footer-colophon-3-col` | 3-column colophon footer |

---

## Style Variations (7 pre-built designs)

### 1. Fossil
- **Colors:** Brownish/neutral (beige base, dark brown contrast)
- **Fonts:** Inter (heading), Cardo (body) — SWAPPED from default
- **Font Sizes:** Larger scale (1rem, 1.2rem, 2rem, 2.65rem, 3.5rem)
- **Buttons:** 100px border-radius (pill), 2px border outline
- **Style:** Neutral earth tones, elegant feel

### 2. Ice
- **Colors:** Cool blue palette (light ice base, dark ink contrast)
- **Fonts:** Inter (heading), Jost (body) — introduces Jost sans-serif
- **Buttons:** 4px radius, uppercase text, 0.75rem, letter-spacing 0.1rem
- **Style:** Cold blue tones, 12 unique gradients, modern tech aesthetic

### 3. Maelstrom
- **Colors:** Dark blue base (#040D3C), white contrast
- **Fonts:** Cardo (body), Jost (heading) — serif body + sans heading
- **Buttons:** 6px radius
- **Style:** Dark blue background with white text, no custom duotones

### 4. Mint
- **Colors:** Light mint/green base, black contrast
- **Fonts:** Instrument Sans (heading), Jost (body) — new modern sans pairing
- **Style:** Clean modern sans-serif, custom heading sizes for h1-h5

### 5. Rust
- **Colors:** Minimal palette (beige base, rust contrast)
- **Duotones:** 1 custom (dark rust to beige)
- **Gradients:** 4 custom (transparent rust, hard transitions)
- **Style:** Minimal, transparent gradient overlays, rust/orange accent

### 6. Ember
- **Colors:** Warm (warm base, black contrast, orange accent)
- **Fonts:** Instrument Sans (body), Jost (heading)
- **Duotones:** 1 custom (orange and white), applied to images by default
- **Gradients:** 12 warm transitions (beige to orange/brown)
- **Style:** Warm aesthetic with default duotone filter on images

### 7. Onyx
- **Colors:** Dark grey base, light contrast, extensive 10-color accent palette
- **Duotones:** 5 custom (dark gray paired with earth tones)
- **Gradients:** 12 dark transitions
- **Style:** Dark mode, most extensive palette of all variations

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

## Per-Block Default Styles (29 blocks configured)

### Navigation & Site Identity

| Block | Key Styles |
|-------|-----------|
| `core/navigation` | Links: no underline, underline on hover. Font weight: 500 |
| `core/site-title` | Font: `body` family, 1.2rem, weight 600. Link: no underline (no change on hover) |
| `core/site-tagline` | Color: `contrast-2`, font size: small |

### Post Content

| Block | Key Styles |
|-------|-----------|
| `core/post-title` | Link: no underline, underline on hover |
| `core/post-author` | Font size: small |
| `core/post-author-name` | Font size: small. Link: no underline, underline on hover |
| `core/post-date` | Color: `contrast-2`, font size: small. Link: `contrast-2`, no underline, underline on hover |
| `core/post-excerpt` | Line height: 1.6 |
| `core/post-terms` | Font size: small. Link: no underline, underline on hover. CSS: prefix color override |
| `core/post-featured-image` | Border radius: `spacing-20` |
| `core/post-navigation-link` | — (default styles) |

### Comment Blocks

| Block | Key Styles |
|-------|-----------|
| `core/comment-author-name` | Color: contrast, font size: small, weight: 600. Link: no underline, underline on hover |
| `core/comment-content` | Font size: small, margin top/bottom: `spacing-20` |
| `core/comment-date` | Color: `contrast-2`, font size: small |
| `core/comment-edit-link` | Font size: small. Link: `contrast-2` |
| `core/comment-reply-link` | Font size: small |
| `core/post-comments-form` | Input border-radius: 0.33rem |
| `core/comments-pagination` | Font size: small (all pagination variants) |

### Content Blocks

| Block | Key Styles |
|-------|-----------|
| `core/code` | Border: `contrast`, radius: `spacing-20`. Bg: `base-2`, text: `contrast-2`. Font: medium, weight 400, line-height 1.6. Padding: `calc(spacing-30 + 0.75rem)` |
| `core/quote` | Bg: `base-2`, border-radius: `spacing-20`. Font: `heading` family, large, italic, line-height 1.3. **Plain variation:** transparent bg, no border, `body` family, medium, normal |
| `core/pullquote` | Font: `heading` family, `x-large`, italic, weight 400, line-height 1.5. Border radius: `spacing-20`. Padding: `spacing-40` top/bottom. Cite: `body` family, medium, normal |
| `core/separator` | 1px solid bottom border, color: `contrast`. Non-full-width: `spacing-60` max-width |
| `core/image` | **Rounded variation:** border-radius: `spacing-20` |
| `core/avatar` | Border radius: 90px (circular) |
| `core/gallery` | Margin bottom: `spacing-50` |
| `core/list` | Padding left: `spacing-10` |
| `core/footnotes` | Font size: small |
| `core/calendar` | Custom CSS for table styling |
| `core/categories` | Padding left/right: 0px, custom list styling |
| `core/search` | Input: 0.33rem border-radius. Button: inherits border-radius. Font size: small |
| `core/loginout` | Custom CSS: border-radius 0.33rem, padding, 1px border |
| `core/query-title` | Custom CSS for italic span styling |
| `core/query-no-results` | Padding top: `spacing-30` |

### Captions

| Element | Key Styles |
|---------|-----------|
| Caption | Color: `contrast-2`, font: `body` family, 0.8rem |

---

## Style Variation — Full Details

### Fossil

**Fonts:** Body=Cardo (serif), Heading=Inter (sans) — swapped from default
**Font Sizes:** small=1rem, medium=1.2rem, large=1.5–2rem fluid, x-large=2–2.65rem fluid, xx-large=2.65–3.5rem fluid
**Gradients (12):** Earth tones — E1DFDB, D6D2CE, 958D86, 65574E, 1A1514 (soft + hard variants)

| Block/Element | Override |
|---------------|----------|
| `core/button` outline | padding: calc(0.9rem-2px), border-width: 2px |
| `core/pullquote` | size: large, fontStyle: normal, weight: normal, line-height: 1.2 |
| `core/quote` | font-family: heading, size: large, fontStyle: normal. Plain: weight 400 |
| `core/site-title` | weight: 400 |
| button element | radius: 100px (pill), bg: contrast-2, text: white, padding: 0.9rem 2rem, font-family: heading, size: small. Hover: bg=contrast |
| heading element | weight: normal, letter-spacing: 0 |

### Ice

**Fonts:** Body=Jost (sans), Heading=Inter (sans)
**Font Sizes:** Same as Fossil (1rem, 1.2rem, 2rem, 2.65rem, 3.5rem)
**Gradients (12):** Cold blues — cbd9e1, EBEBEF, 466577, 37505d, 1C2930 (soft + hard variants)

| Block/Element | Override |
|---------------|----------|
| `core/button` outline | padding: calc(1rem-1px) calc(2.2rem-1px), border-width: 1px |
| `core/pullquote` | size: large, fontStyle: normal, weight: normal, line-height: 1.2 |
| `core/quote` | font-family: heading, size: large, fontStyle: normal. Plain: weight 400 |
| `core/site-title` | weight: 400 |
| button element | radius: 4px, bg: contrast-2, text: white, padding: 1rem 2.2rem, size: 0.75rem, uppercase, letter-spacing: 0.1rem. Hover: bg=contrast |
| heading element | weight: normal, letter-spacing: 0 |

### Maelstrom

**Fonts:** Body=Cardo (serif), Heading=Jost (sans)
**Font Sizes:** Same as Fossil
**Gradients:** None

| Block/Element | Override |
|---------------|----------|
| `core/button` outline | padding: calc(0.8rem-2px) calc(1.6rem-2px), border-width: 2px |
| `core/site-title` | font-family: heading, weight: normal |
| `core/navigation` | size: small, weight: normal |
| button element | radius: 6px, bg: contrast, text: base-2, padding: 0.8rem/0.98rem 1.6rem, font-family: heading, size: small. Hover: bg=contrast |
| heading element | font-family: heading, letter-spacing: 0 |

### Mint

**Fonts:** Body=Jost (sans), Heading=Instrument Sans (sans)
**Gradients:** None

| Block/Element | Override |
|---------------|----------|
| `core/navigation` | fontStyle: normal, weight: 400 |
| `core/pullquote` | font-family: body, size: x-large, fontStyle: normal, weight: 600, line-height: 1.3 |
| `core/quote` | font-family: body, size: large, fontStyle: normal, weight: 400 |
| `core/site-title` | font-family: heading |
| caption element | font-family: body |
| h1 | size: x-large |
| h2 | size: 2.1rem |
| h3 | size: large |
| h4 | size: 1.6rem |
| h5 | size: 1.4rem |
| heading element | font-family: heading, fontStyle: normal, weight: 600 |

### Rust

**Duotone:** `duotone-1` — #A62B0C, #F3F0E7 ("Dark rust to beige")
**Gradients (4):** gradient-1: transparent rust→beige, gradient-7: hard transparent, gradient-2: solid rust→beige, gradient-8: hard solid

| Block/Element | Override |
|---------------|----------|
| `core/calendar` | Custom CSS: th bg=contrast, text=base, border=contrast; td border=contrast |
| `core/comment-date` | text: contrast, link text: contrast |
| `core/comment-edit-link` | link text: contrast |
| `core/comment-reply-link` | link text: contrast |
| `core/post-date` | text: contrast, link text: contrast |
| `core/post-terms` | CSS: prefix color=contrast |
| `core/quote` | bg: base |
| `core/site-tagline` | text: contrast |
| button :hover/:focus | bg: contrast, border: contrast |
| caption element | text: contrast |

### Ember

**Fonts:** Body=Instrument Sans (sans), Heading=Jost (sans)
**Duotone:** `duotone-2` — #D73301, #F9F8F5 ("Orange and white")
**Gradients (12):** Warm tones — f6decd, dbab88, A4A4A4, 353535, 111111 (soft + hard variants)

| Block/Element | Override |
|---------------|----------|
| `core/button` outline | padding: calc(0.9rem-2px), border-width: 2px |
| `core/image` | duotone filter: duotone-2 |
| `core/pullquote` | size: large, fontStyle: normal, weight: normal, line-height: 1.2 |
| `core/quote` | font-family: heading, size: large, fontStyle: normal. Plain: weight 400 |
| `core/site-title` | weight: 400 |
| `core/navigation` | weight: 400 |
| button element | radius: 100px (pill), bg: contrast-2, text: base, padding: 0.9rem 2rem, font-family: heading, size: small. Hover: bg=contrast |

### Onyx

**Duotones (5):** All #272727 paired with: #f9f9f9 (white), #5F584F (walnut), #973C20 (cinnamon), #4D5B48 (olive), #4F5959 (steel)
**Gradients (12):** Dark tones — 5F584F, 6D533C, 973C20, 4D5B48, 4F5959, 909090, 272727 (soft + hard variants)
**No block/element overrides** — uses default styles with dark palette only
