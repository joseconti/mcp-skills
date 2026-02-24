# Twenty Twenty-Five — Complete Configurable Options

All values below are the **theme.json defaults**. User overrides are stored in Global Styles (`wp_global_styles` post type). Use `var:preset|{type}|{slug}` format to reference presets in styles.

---

## Global Settings

| Setting | Value | Description |
|---------|-------|-------------|
| `appearanceTools` | `true` | Enables all appearance editing tools |
| `useRootPaddingAwareAlignments` | `true` | Full-width blocks honor root padding |
| `typography.fluid` | `true` | Responsive fluid typography enabled |
| `typography.writingMode` | `true` | RTL language support |
| `color.defaultDuotone` | `false` | Only custom duotones (none in base) |
| `color.defaultGradients` | `false` | Only custom gradients (none in base) |
| `color.defaultPalette` | `false` | Only custom palette |
| `spacing.defaultSpacingSizes` | `false` | Custom spacing scale |
| `typography.defaultFontSizes` | `false` | Custom font sizes |

---

## Color Palette (8 colors)

| Name | Slug | Default | CSS Variable |
|------|------|---------|-------------|
| Base | `base` | `#FFFFFF` | `--wp--preset--color--base` |
| Contrast | `contrast` | `#111111` | `--wp--preset--color--contrast` |
| Accent 1 | `accent-1` | `#FFEE58` (yellow) | `--wp--preset--color--accent-1` |
| Accent 2 | `accent-2` | `#F6CFF4` (light pink) | `--wp--preset--color--accent-2` |
| Accent 3 | `accent-3` | `#503AA8` (purple) | `--wp--preset--color--accent-3` |
| Accent 4 | `accent-4` | `#686868` (gray) | `--wp--preset--color--accent-4` |
| Accent 5 | `accent-5` | `#FBFAF3` (off-white) | `--wp--preset--color--accent-5` |
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

### Font Families (base theme: 2)

| Name | Slug | Font Stack | Weight Range |
|------|------|-----------|-------------|
| Manrope | `manrope` | `Manrope, sans-serif` | 200–800 (variable) |
| Fira Code | `fira-code` | `"Fira Code", monospace` | 300–700 (variable) |

**Default body font:** `manrope`

### Additional Fonts in Style Variations

| Font | Slug | Used In | Type |
|------|------|---------|------|
| Beiruti | `beiruti` | Noon | Sans-serif, 200–900 |
| Literata | `literata` | Noon, Morning, Sunrise, Midnight | Serif, 200–900 |
| Vollkorn | `vollkorn` | Dusk | Serif, 400–900 |
| Platypi | `platypi` | Afternoon, Sunrise | Sans-serif, 300–800 |
| Ysabeau Office | `ysabeau-office` | Afternoon, Morning | Sans-serif, 100–900 |
| Roboto Slab | `roboto-slab` | Twilight | Serif, 100–900 |
| Fira Sans | `fira-sans` | Midnight | Sans-serif, 100–900 |

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

| Heading | Font Size | Additional |
|---------|-----------|------------|
| H1 | `var:preset|font-size|xx-large` | — |
| H2 | `var:preset|font-size|x-large` | — |
| H3 | `var:preset|font-size|large` | — |
| H4 | `var:preset|font-size|medium` | — |
| H5 | `var:preset|font-size|small` | letter-spacing: 0.5px |
| H6 | `var:preset|font-size|small` | weight: 700, letter-spacing: 1.4px, uppercase |

---

## Layout

| Property | Value |
|----------|-------|
| Content Size | 645px |
| Wide Size | 1340px |

---

## Spacing

### Spacing Scale (7 sizes)

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

### Default Templates

| File | Purpose | Key Content |
|------|---------|-------------|
| `index.html` | Blog listing | Hidden blog heading + query loop pattern |
| `home.html` | Front page | Hidden blog heading + query loop pattern |
| `single.html` | Single post | Title + featured image (3:2) + written-by pattern + content + tags + nav + comments + more-posts |
| `page.html` | Single page | Featured image + title + content |
| `archive.html` | Archive | Query title + term description + query loop |
| `search.html` | Search | Query title + search + query loop + more-posts |
| `404.html` | Error page | Hidden-404 pattern |
| `page-no-title.html` | Page without title | Content only (constrained, locked) |

### Template Parts (7)

| Title | Slug | Area | Content |
|-------|------|------|---------|
| Header | `header` | header | Site title + navigation |
| Vertical site header | `vertical-header` | header | Vertical/sidebar header layout |
| Header with large title | `header-large-title` | header | Prominent title header |
| Footer | `footer` | footer | Standard footer |
| Footer Columns | `footer-columns` | footer | Multi-column footer |
| Footer Newsletter | `footer-newsletter` | footer | Footer with newsletter signup |
| Sidebar | `sidebar` | uncategorized | Sidebar widget area |

---

## Post Formats

Supported: `aside`, `audio`, `chat`, `gallery`, `image`, `link`, `quote`, `status`, `video`

---

## Custom Block Styles

### From functions.php

| Block | Style Slug | Label | CSS |
|-------|-----------|-------|-----|
| `core/list` | `checkmark-list` | Checkmark | `list-style-type: "\2713"; li { padding-inline-start: 1ch }` |

### From styles/blocks/ (JSON-defined)

| Style Slug | Title | Applies To | Key Styles |
|------------|-------|-----------|------------|
| `text-display` | Display | `core/heading`, `core/paragraph` | fontSize: `clamp(2.2rem, 2.2rem + ((1vw - 0.2rem) * 1.333), 3.5rem)`, lineHeight: 1.2 |
| `text-subtitle` | Subtitle | `core/heading`, `core/paragraph` | fontSize: `clamp(1.5rem, 1.5rem + ((1vw - 0.2rem) * 0.392), 1.75rem)`, lineHeight: 1.2 |
| `text-annotation` | Annotation | `core/heading`, `core/paragraph` | fontSize: small, lineHeight: 1.5, border: 1px solid currentColor, radius: 16px, padding: 0.2rem 0.6rem, width: fit-content, link: no underline |
| `post-terms-1` | Pill shaped | `core/post-terms` | link border: 0.8px solid accent-6, radius: 20px, padding: 5px 10px, fontWeight: 400, lineHeight: 2.8, no underline, underline on :hover |

### Section Style Variations (from styles/sections/)

Applied to `core/group`, `core/columns`, `core/column` via `.is-style-section-N` class:

| Section | Background | Text | Key Overrides |
|---------|-----------|------|---------------|
| `section-1` | accent-5 | contrast | Separator: 25% currentColor. Post-date: 85% currentColor. All post/comment blocks: currentColor. Pullquote/quote: currentColor |
| `section-2` | accent-2 | base | Similar to section-1 with different color mapping |
| `section-3` | accent-3 | base | Similar to section-1 with different color mapping |
| `section-4` | contrast | base | Similar to section-1 with different color mapping |
| `section-5` | accent-1 | contrast | Similar to section-1 with different color mapping |

Each section overrides: `core/separator`, `core/site-title`, `core/post-author-name`, `core/post-date`, `core/post-terms`, `core/comment-author-name`, `core/comment-date`, `core/comment-edit-link`, `core/comment-reply-link`, `core/pullquote`, `core/quote` — setting text and link colors to `currentColor` for consistency.

---

## Block Patterns (98 total)

### Header Patterns

| Slug | Description |
|------|-------------|
| `header` | Default site header |
| `vertical-header` | Vertical/sidebar header |
| `header-large-title` | Header with prominent title |
| `header-centered` | Centered header |
| `header-columns` | Multi-column header |

### Footer Patterns

| Slug | Description |
|------|-------------|
| `footer` | Standard footer |
| `footer-columns` | Multi-column footer |
| `footer-newsletter` | Footer with newsletter signup |
| `footer-centered` | Centered footer |
| `footer-social` | Footer with social links |

### Blog Query Patterns

| Slug | Description |
|------|-------------|
| `template-query-loop` | Standard post query loop |
| `template-query-loop-text-blog` | Text-focused blog |
| `template-query-loop-photo-blog` | Photo-focused blog |
| `template-query-loop-news-blog` | News-style blog |
| `template-query-loop-vertical-header-blog` | Query with vertical header |

### Template Patterns (home, single, archive, search, 404)

| Prefix | Description | Variants |
|--------|-------------|----------|
| `template-home-*` | Home page templates | news-blog, photo-blog, text-blog, vertical-header-blog, with-sidebar, posts-grid |
| `template-single-*` | Single post templates | news-blog, photo-blog, text-blog, vertical-header-blog, offset, left-aligned |
| `template-archive-*` | Archive templates | news-blog, photo-blog, text-blog, vertical-header-blog |
| `template-search-*` | Search templates | news-blog, photo-blog, text-blog, vertical-header-blog |
| `template-404-*` | 404 templates | vertical-header-blog |

### Hero/Banner Patterns

| Slug | Description |
|------|-------------|
| `hero-full-width-image` | Full-width hero with image |
| `hero-book` | Book/product hero |
| `hero-podcast` | Podcast hero |
| `banner-intro` | Introduction banner |
| `banner-intro-image` | Banner with image |
| `banner-poster` | Poster-style banner |

### Content Section Patterns

| Category | Examples |
|----------|---------|
| CTA/Marketing | `cta-centered-heading`, `cta-newsletter`, `cta-events-list`, `cta-book-links` |
| Services/Business | `services-3-col`, `services-team-photos`, `page-business-home` |
| Testimonials | `testimonials-2-col`, `testimonials-6-col`, `testimonials-large` |
| Pricing | `pricing-2-col`, `pricing-3-col` |
| Events | `event-3-col`, `event-schedule`, `event-rsvp` |
| Media | `media-instagram-grid`, `grid-videos`, `logos` |

### Landing Page Patterns

| Slug | Description |
|------|-------------|
| `page-landing-book` | Book landing page |
| `page-landing-event` | Event landing page |
| `page-landing-podcast` | Podcast landing page |
| `page-coming-soon` | Coming soon page |
| `page-cv-bio` | CV/bio page |
| `page-link-in-bio-*` | Link-in-bio pages (3 variants) |

### Hidden/Utility Patterns

| Slug | Purpose |
|------|---------|
| `hidden-blog-heading` | Blog page heading |
| `hidden-search` | Search heading |
| `hidden-404` | 404 content |
| `hidden-written-by` | Author metadata |
| `hidden-sidebar` | Sidebar area |
| `post-navigation` | Previous/next post navigation |
| `comments` | Comments section |
| `more-posts` | "Read more" CTA section |

---

## Style Variations (8 pre-built designs)

### 1. Evening (dark theme)
- **Colors:** Base `#1B1B1B`, Contrast `#F0F0F0`, Accent 1 `#786D0A` (olive), Accent 2 `#442369` (purple), Accent 5 `#353535`
- **Fonts:** Base theme fonts (Manrope + Fira Code)
- **Style:** Dark background, light text, subtle accents

### 2. Noon (elegant light)
- **Colors:** Base `#F8F7F5` (cream), Contrast `#191919`, Accent 1 `#FFFFFF`, Accent 2 `#F5B684` (peach)
- **Fonts:** Beiruti (sans, 200–900) + Literata (serif, 200–900)
- **Style:** Elegant serif body (Literata), Beiruti for buttons/site title, shadow on buttons

### 3. Dusk (purple/tech)
- **Colors:** Base `#E2E2E2`, Contrast `#3B3B3B`, Accent 1 `#F5EDFF` (light purple), Accent 2 `#650DD4` (vibrant purple)
- **Fonts:** Vollkorn (serif, 400–900) + Fira Code (mono)
- **Style:** Monospace body (Fira Code), Vollkorn serif headings, purple accent, custom h1-h5 pixel sizes

### 4. Afternoon (green/nature)
- **Colors:** Base `#DAE7BD` (sage), Contrast `#516028` (dark green), Accent 1 `#C7F642` (lime)
- **Fonts:** Platypi (sans, 300–800) + Ysabeau Office (sans, 100–900)
- **Style:** Nature palette, Ysabeau Office body, Platypi headings, sharp buttons (no radius), uppercase site title

### 5. Twilight (dark blue/orange)
- **Colors:** Base `#131313`, Contrast `#FFFFFF`, Accent 1 `#4B52FF` (blue), Accent 2 `#FF7A5C` (coral)
- **Fonts:** Roboto Slab (serif, 100–900) + Manrope (sans)
- **Style:** Dark theme, uppercase navigation + buttons, Roboto Slab headings (weight 300)

### 6. Morning (blue/beige)
- **Colors:** Base `#DFDCD7` (beige), Contrast `#191919`, Accent 1 `#7A9BDB` (blue), Accent 3 `#182949` (dark blue)
- **Fonts:** Literata (serif, 200–900) + Ysabeau Office (sans)
- **Style:** Ysabeau Office body, Literata headings (weight 900), blue accent buttons

### 7. Sunrise (warm/tropical)
- **Colors:** Base `#330616` (dark burgundy), Contrast `#FFFFFF`, Accent 1 `#F0FDA6` (pale yellow), Accent 2 `#DB9AB1` (dusty rose)
- **Fonts:** Platypi (sans, 300–800) + Literata (serif)
- **Style:** Dark burgundy base, Literata body (1.5rem), Platypi headings (weight 800), large typography

### 8. Midnight (neon/cyberpunk)
- **Colors:** Base `#4433A6` (deep purple), Contrast `#79F3B1` (neon cyan), Accent 5 `#E8B7FF` (magenta)
- **Fonts:** Literata (serif, 200–900) + Fira Sans (sans, 100–900)
- **Duotone:** Midnight filter (`#4433A6` → `#79F3B1`) applied to images, avatars, covers, logos
- **Style:** Cyberpunk neon, Fira Sans body, Literata headings (weight 200), uppercase buttons

### Section Variations

All 8 style variations define `styles.variations` with numbered section styles (`section-1` through `section-5`, plus `post-terms-1`). These apply different colors to Group blocks using `.wp-block-group.is-style-section-N` classes.

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
| Focus Outline | 2px solid `accent-4`, offset 2px |

### Outline Variation

| Property | Value |
|----------|-------|
| Border | `1px solid currentColor` |
| Padding | `calc(1rem - 1px) calc(2.25rem - 1px)` |
| Hover Background | `color-mix(in srgb, var(--wp--preset--color--contrast) 5%, transparent)` |

---

## Link Styles

| State | Color | Text Decoration |
|-------|-------|----------------|
| Default | `currentColor` | inherited |
| Hover | — | none |

---

## Per-Block Default Styles (30+ blocks configured)

### Navigation & Site Identity

| Block | Key Styles |
|-------|-----------|
| `core/navigation` | Font size: medium. Links: no underline, underline on hover |
| `core/site-title` | Weight: 700, letter-spacing: -0.5px. Link: no underline, underline on hover |
| `core/site-tagline` | Font size: medium |

### Post Content

| Block | Key Styles |
|-------|-----------|
| `core/post-title` | Link: no underline, underline on hover |
| `core/post-date` | Color: `accent-4`, font size: small. Link: no underline, underline on hover |
| `core/post-terms` | Font size: small, weight: 600. CSS: `a { white-space: nowrap }` |
| `core/post-navigation-link` | Font size: medium |

### Comment Blocks

| Block | Key Styles |
|-------|-----------|
| `core/comment-author-name` | Color: `accent-4`, font size: small |
| `core/comment-content` | Font size: medium |
| `core/comment-date` | Font size: small, color: contrast |
| `core/comment-edit-link` | Font size: small |
| `core/comment-reply-link` | Font size: small |
| `core/post-comments-form` | Custom CSS for textarea/input styling |
| `core/comments-pagination` | Font size: medium, weight: 500 |

### Content Blocks

| Block | Key Styles |
|-------|-----------|
| `core/code` | Font: `fira-code`, medium, weight 300. Bg: `accent-5`. Padding: `spacing-40` |
| `core/quote` | Left border: 2px solid currentColor. Font: large, weight 300. **Plain variation:** no border/padding |
| `core/pullquote` | Font: `xx-large`, weight 300, line-height 1.2. Cite: small, normal |
| `core/separator` | 1px solid bottom, color: `accent-6` |
| `core/avatar` | Border radius: 100px |
| `core/search` | Input/button: rounded (3.125rem), input border: `accent-6` |
| `core/columns` | Block gap: `spacing-50` |
| `core/buttons` | Block gap: 16px |
| `core/list` | CSS: `li { margin-top: 0.5rem }` |
| `core/query-pagination` | Font size: medium, weight: 500 |
| `core/term-description` | Font size: medium |

---

## Style Variation — Per-Block Overrides

Each variation overrides block-level and element-level styles beyond just the color palette. Below are the **unique block/element changes** per variation (colors/fonts are listed in the Style Variations section above):

### Evening
- `core/button` outline: padding adjusted (0.6rem top/bottom, 1.6rem left/right)
- Section-2 button: bg=base, text=contrast
- Section-4 button: bg=accent-2, text=contrast

### Noon
**Custom font sizes:** Small 0.9rem, Medium 1–1.2rem fluid, Large 1.6–1.8rem fluid, X-Large 1.8–2.2rem fluid, XX-Large 2–2.8rem fluid

| Block/Element | Override |
|---------------|----------|
| `core/button` | border-color: contrast, shadow: natural, font-family: beiruti |
| `core/button` outline | shadow: none |
| `core/list` | line-height: 1.3 |
| `core/loginout` | font-size: medium |
| `core/post-terms` | font-weight: 300 |
| `core/post-title` | text: accent-3, link: currentColor |
| `core/pullquote` | text: accent-3, font-family: beiruti, weight: 500, line-height: 1 |
| `core/quote` | font-size: medium |
| `core/query-pagination` | font-weight: 300 |
| `core/query-title` | text: accent-3, link: currentColor |
| `core/site-tagline` | font-size: small |
| `core/site-title` | font-family: beiruti, weight: 600, letter-spacing: 2.4px, uppercase |
| heading element | color: accent-3, font-family: beiruti, weight: 500, letter-spacing: -0.02em, line-height: 1.02 |
| h4 | font-size: large |
| h5 | font-size: medium, letter-spacing: 0px |
| h6 | font-size: small |

### Dusk
**Custom color:** `settings.custom.color.accent-2-opacity-20` = `#650DD433`

| Block/Element | Override |
|---------------|----------|
| `core/code` | text: black, bg: accent-5 |
| `core/paragraph` | link text: accent-2 |
| `core/post-author-name` | weight: 300, text: accent-2 |
| `core/post-terms` | weight: 300, text: accent-2 |
| `core/post-title` | weight: 400, letter-spacing: -0.96px, link: accent-3 |
| `core/pullquote` | text: black, font-family: vollkorn, size: x-large, weight: 400. Cite: font-family: fira-code, weight: 300 |
| `core/quote` | text: black, font-family: fira-code, weight: 500, letter-spacing: -0.18px |
| `core/site-title` | text: accent-3, font-family: vollkorn, size: x-large |
| button element | font-family: fira-code, size: medium, weight: 400, bg: accent-2, text: base, radius: 4px |
| heading element | text: accent-3, font-family: vollkorn |
| h1–h5 | fixed pixel sizes (48, 38, 32, 28, 24px) with letter-spacing |
| link element | text: accent-3 |
| post-terms-1 variation | link border: accent-2-opacity-20, radius: 4px |

### Afternoon
**Custom font sizes:** Small 0.875rem, Medium 1–1.125rem fluid, Large 1.125–1.375rem fluid, X-Large 1.4–1.8rem fluid, XX-Large 2–2.6rem fluid

| Block/Element | Override |
|---------------|----------|
| `core/button` | border-radius: 0px, padding: 1rem 1.6rem |
| `core/code` | letter-spacing: 0px |
| `core/heading` | line-height: 1.2 |
| `core/list` | line-height: 1.3 |
| `core/loginout` | font-size: medium |
| `core/post-terms` | font-weight: 400 |
| `core/pullquote` | font-family: platypi, letter-spacing: -0.01em, line-height: 1.1 |
| `core/quote` | font-weight: 300 |
| `core/site-title` | font-family: ysabeau-office, size: large, letter-spacing: 1.44px, uppercase |
| button element | font-family: ysabeau-office, weight: 600, letter-spacing: 1.44px, uppercase |
| heading element | font-family: platypi |
| h5 | font-size: medium |
| h6 | font-size: small, weight: 400 |

### Twilight
**Custom font sizes:** Small 0.875rem, Medium 1–1.125rem fluid, Large 1.125–1.375rem fluid, X-Large 1.75–2rem fluid, XX-Large 2.15–2.4rem fluid

| Block/Element | Override |
|---------------|----------|
| `core/button` outline | padding: 0.625rem 1.375rem |
| `core/navigation` | font-size: large, letter-spacing: -0.28px, uppercase |
| `core/post-author` | font-size: small |
| `core/post-author-name` | font-size: small |
| `core/post-terms` | font-weight: 500 |
| `core/pullquote` | font-family: roboto-slab, size: xx-large, weight: 200 |
| `core/search` | uppercase |
| `core/site-tagline` | font-size: large |
| `core/site-title` | uppercase |
| button element | padding: 0.625rem 1.375rem, weight: 500, letter-spacing: -0.36px, uppercase |
| heading element | font-family: roboto-slab, weight: 300, letter-spacing: -0.5px, line-height: 1.2 |
| Section-5 | Custom CSS for `core/post-comments-form` (textarea/input border-radius) and `core/search` (input border-color) |

### Morning

| Block/Element | Override |
|---------------|----------|
| `core/code` | text: contrast, bg: accent-5 |
| `core/navigation` | font-size: 1.25rem |
| `core/paragraph` | link: contrast |
| `core/post-author-name` | link: contrast |
| `core/post-title` | weight: 900, letter-spacing: -0.96px, link: contrast |
| `core/pullquote` | text: contrast, size: xx-large. Cite: size: medium |
| `core/quote` cite | size: medium, color: accent-4 |
| `core/query-title` | weight: 900 |
| `core/site-title` | font-family: ysabeau-office, uppercase, letter-spacing: 1.6px |
| button element | font-family: literata, size: medium, weight: 900, bg: accent-1, text: contrast, radius: 0px |
| heading element | font-family: literata, weight: 900, line-height: 1.2 |
| post-terms-1 variation | font-size: medium, link bg: accent-5, border: radius 100px, color accent-5 |

### Sunrise

| Block/Element | Override |
|---------------|----------|
| `core/code` | text: accent-2, bg: accent-5 |
| `core/navigation` | font-size: 1.25rem |
| `core/post-author-name` | text: contrast |
| `core/post-terms` | weight: 400, text: contrast |
| `core/post-title` | weight: 800, letter-spacing: -0.96px, link: accent-2 |
| `core/pullquote` | text: accent-2, font-family: platypi, size: x-large, weight: 800. Cite: font-family: literata, weight: 400 |
| `core/quote` | text: accent-2, size: 1.5rem, weight: 600, letter-spacing: -0.24px |
| `core/site-title` | font-family: platypi, size: 30px, weight: 800, letter-spacing: -0.6px |
| button element | text: base, bg: accent-2, radius: 0px, font-family: platypi, size: 1.5rem, weight: 800 |
| heading element | font-family: platypi, weight: 800 |
| link element | text: contrast |
| post-terms-1 variation | font-size: 16px, link bg: accent-5, border: radius 100px, color accent-5 |

### Midnight
**Custom duotone:** `midnight-filter` (`#4433A6` → `#79F3B1`) — applied to avatar, cover, image, post-featured-image, site-logo
**Custom font sizes:** Small 0.9rem, Medium 0.9–1.2rem fluid, Large 1.2–1.8rem fluid, X-Large 1.8–2.2rem fluid, XX-Large 2–2.8rem fluid

| Block/Element | Override |
|---------------|----------|
| `core/avatar` | duotone filter: midnight-filter |
| `core/button` outline | padding: 1rem all sides |
| `core/code` | bg: accent-2, text: contrast |
| `core/cover` | duotone filter: midnight-filter |
| `core/image` | duotone filter: midnight-filter |
| `core/post-date` | text: contrast, link: contrast |
| `core/post-featured-image` | duotone filter: midnight-filter |
| `core/post-title` | weight: 200 |
| `core/pullquote` | border: none, font-family: literata, weight: 200 |
| `core/query-pagination` | weight: 300 |
| `core/quote` | size: medium, letter-spacing: -0.01em, line-height: 1.5, weight: 300 |
| `core/search` | border-radius: 0px |
| `core/site-logo` | duotone filter: midnight-filter |
| `core/site-title` | font-family: literata, size: x-large, weight: 300, letter-spacing: -0.56px, uppercase |
| button element | radius: 0px, bg: contrast, text: base, padding: 1rem all, font-family: literata, size: medium, weight: 400, letter-spacing: -0.01em, uppercase |
| heading element | font-family: literata, weight: 200, letter-spacing: -0.02em, line-height: 1.24 |
| h6 | weight: 200 |
