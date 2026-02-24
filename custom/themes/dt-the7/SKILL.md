---
name: dt-the7
description: "Use when configuring The7 WordPress theme (Dream-Theme). Provides all available options (colors, typography, header, footer, layout, blog, portfolio, buttons, page titles, mobile header, floating header, micro-widgets, stripes, social buttons, advanced settings) and procedures to apply them via MCP Content Manager abilities. Classic theme — theme options stored in wp_options as the7. Logo uses WordPress custom_logo theme mod."
compatibility: "The7 14.2+. Requires WordPress 6.6+ and PHP 7.2+. Classic theme (NOT FSE)."
---

# The7 Theme Configuration

## Theme Type

**Classic theme (NOT Full Site Editing)**. Configuration is split between two storage mechanisms:

1. **Theme options** (`the7` in `wp_options`): Colors, typography, layout, footer, buttons, page titles, sidebar, blog, portfolio, image hovers, loading effects, contact form. Read/write via `mcm/get-theme-options` and `mcm/set-theme-options`.
2. **Theme mods** (`theme_mods_dt-the7` in `wp_options`): Logo (`custom_logo`), navigation menu locations. Read/write via `mcm/get-theme-mod` and `mcm/set-theme-mod`.

Does NOT use Global Styles or theme.json. Uses a custom Options Framework with `of_get_option()` accessor.

## When to use

- The user wants to change colors, fonts, header, footer, or layout of The7
- The user wants to configure blog, portfolio, or sidebar settings
- The user wants to adjust buttons, page titles, or image hover effects
- The user wants to set up logo, favicons, and branding
- The user wants to set up the site identity
- The user wants to configure mobile header, floating header, or top bar
- The user wants to add header micro-widgets (social icons, search, buttons, text, login, menus)
- The user wants to configure social sharing buttons on posts/portfolio
- The user wants to set up decorative stripes/background sections
- The user wants to adjust advanced settings (lazy loading, smooth scroll, custom CSS, tracking code)
- The user wants to configure widget areas or sidebar assignments

## Inputs required

- What aspect to configure (colors, typography, header, footer, layout, blog, buttons, or all)
- The desired values (specific colors, font choices, sizes, etc.)

## CRITICAL: Setup Workflow (Follow This Order)

When configuring The7 from scratch, follow this exact order to avoid missing settings:

1. **Site identity**: Set blog name, tagline, homepage, posts page
2. **Logo (theme mod)**: Upload logo → set `custom_logo` via `mcm/set-theme-mod`
3. **Favicon (theme option)**: Set favicon and retina favicon in `the7`
4. **Colors**: Set accent color mode FIRST, then accent color, then body/text/header colors
5. **Typography**: Set body font, heading font, H1-H6 sizes
6. **Layout**: Set site width, layout mode (wide/boxed), content margins
7. **Header**: Set header layout, background mode, colors, decoration
8. **Mobile header**: Set breakpoints, layouts, mobile menu style
9. **Floating header**: Enable/configure sticky floating navigation
10. **Top bar**: Set top bar height, background, content (if needed)
11. **Micro-widgets**: Configure header micro-widgets (social, search, buttons, text)
12. **Footer**: Set footer style, colors, layout columns, bottom bar
13. **Page titles**: Set title area style, colors, breadcrumbs, responsive titles
14. **Blog/Portfolio**: Set blog meta, related posts, filters, fancy date
15. **Buttons**: Set button colors, sizes, borders, shadows (5 size variants)
16. **Social buttons**: Configure share button networks, visibility, titles
17. **Advanced**: Set lazy loading, smooth scroll, responsive, custom CSS
18. **Verify**: Check all changes on the frontend

## AI-Guided Configuration Workflow

When configuring The7 from scratch, offer the user **two modes**:

### Mode 1: "Guide me step by step"

Ask the user about each configuration area, one at a time. For each area, present the available options and ask what they prefer:

1. **Colors**: "What is your brand's primary/accent color? Do you want a light or dark site background? What color for headings and body text? The7 uses an accent color system — your accent color is applied to buttons, links, hovers, and highlights across the entire site."

2. **Typography**: "What font do you want for body text? (e.g., Open Sans, Roboto, Lato) What font for headings? (e.g., Montserrat, Playfair Display) What text sizes for headings H1-H6? Default: H1=44px, H2=26px, H3=22px, H4=18px, H5=15px, H6=12px."

3. **Header**: "What header layout do you want?
   - **Classic** — Logo left, navigation right (most common)
   - **Inline** — Logo and navigation on a single line
   - **Split** — Logo centered, navigation split on both sides
   - **Side** — Vertical sidebar header
   - **Top Line** — Navigation in a thin top bar
   - **Side Line** — Minimal side bar with expandable menu
   - **Menu Icon** — Floating hamburger menu button
   - **Disabled** — No header

   Do you want the header to be transparent over the title area? Should it be full-width?"

4. **Mobile Header**: "The7 has two mobile breakpoints:
   - **Tablet** (default: 1024px) — First switch point
   - **Phone** (default: 760px) — Second switch point

   For each, choose a layout: logo left + menu right, logo left + menu centered, logo right + menu left, or logo right + menu centered. What background color for the mobile menu? Should it slide from the left or right?"

5. **Floating Header**: "Do you want a sticky/floating header that appears when scrolling down? Options:
   - Background color (default: semi-transparent white)
   - Height (default: 100px)
   - Use the main logo, a custom logo, or no logo
   - Bottom decoration: shadow, line, or none"

6. **Top Bar**: "Do you want a top bar above the header? This thin bar can contain text, contact info, social icons, or micro-widgets. Set its height (0 disables it), background color, and padding."

7. **Micro-widgets**: "The7 supports 7 types of header micro-widgets that can be placed in various header positions:
   - **Social Icons** — Social media icon links with customizable size, colors, and shapes
   - **Menu** (x2) — Additional navigation menus as dropdown or list
   - **Button** (x2) — CTA buttons with custom text, URL, colors
   - **Login** — Login/logout button with custom icon
   - **Text** (x5) — Free HTML/text content areas
   - **Search** — Search form (popup, overlay, animate-width, or classic)
   - **Multipurpose** (x5) — Address, email, phone, Skype, working hours with icons

   Do you want any micro-widgets in your header?"

8. **Footer**: "How many footer columns? (1-4) What background color? Options:
   - **Style**: Content-width line, full-width line, or solid background
   - **Slide-out footer**: Footer slides out from behind the content on scroll
   - **Bottom bar**: Copyright text, credits, custom text, with its own background"

9. **Page Titles & Breadcrumbs**: "Do you want a title area on pages? Options:
   - **Background mode**: Content line, solid color, gradient, background image (with parallax), or disabled
   - **Title alignment**: Left, center, or right
   - **Title decoration**: None or outline
   - **Breadcrumbs**: Show/hide, with customizable background, border, and typography
   - **Responsive**: Different height and font size on mobile"

10. **Blog**: "Show date, author, categories, comments, tags in blog posts? Show related posts at the end? Options:
    - Fancy date style: circle or square
    - Fancy categories overlay
    - Thumbnail size mode: original or custom proportions
    - Previous/next navigation
    - Back button to blog page
    - Filter style: iOS, minimal, or material"

11. **Buttons**: "Button styling options:
    - **Color mode**: Accent color, custom color, gradient, or disabled
    - **Text color**: Accent or custom
    - **Hover effects**: Different color/gradient on hover
    - **Border**: Custom border color mode and width
    - **Shadows**: Button shadow and hover shadow
    - **Sizes**: 5 button sizes (S, M, L, LG, XL) each with independent typography, min-width, min-height, padding, border radius, and border width"

12. **Social / Share Buttons**: "Do you want social sharing buttons on posts and portfolio items? Options:
    - Visibility: Show on hover or always visible
    - Per-template button titles (posts, portfolio, photos, pages)
    - Supported networks: Facebook, Twitter, LinkedIn, Pinterest, Email, WhatsApp, Telegram, Reddit, and more"

13. **Stripes**: "The7 supports decorative page stripes — background sections with independent colors, images, outlines, and content box styling. Each stripe has its own heading/text colors and content box decoration."

14. **Advanced Settings**: "Fine-tuning options:
    - **Responsive layout**: Enable/disable
    - **Lazy loading**: For images
    - **Smooth scroll**: On, off, or only on parallax pages
    - **Image resize engine**: Fast resize for thumbnails
    - **User scalable**: Allow pinch-to-zoom on mobile
    - **FVM integration**: Fast Velocity Minify plugin support
    - **OpenGraph tags**: Enable/disable The7 OG meta tags
    - **Custom CSS**: Add custom styles
    - **Tracking code**: Google Analytics, tag manager, etc."

### Mode 2: "Design it for me" (AI decides freely)

The user says something like "you decide", "surprise me", "design it for me", or "let the AI choose". In this mode:

1. Ask the user ONLY these 3 things:
   - **Site type**: corporate, creative, ecommerce, blog, portfolio, restaurant, agency
   - **Brand color**: their primary color if they have one (or let AI pick)
   - **General feel**: modern, elegant, minimalist, bold, warm, professional
2. Based on those inputs, the AI designs a complete, coherent theme:
   - Choose a complementary color palette (accent, background, text, footer)
   - Select matching Google Fonts (one for body, one for headings)
   - Pick the best header layout for the site type (e.g., Classic for corporate, Split for creative)
   - Configure mobile header with appropriate breakpoints and slide direction
   - Enable floating header with semi-transparent background
   - Configure footer with appropriate columns and dark background
   - Set typography sizes with good visual hierarchy (H1-H6)
   - Enable breadcrumbs and page titles with matching colors
   - Configure buttons in accent mode with white text
   - Set up social share buttons for posts
   - Configure advanced settings (lazy loading, smooth scroll)
   - If applicable, check for FSE skins that match the site type
3. Apply ALL settings in one batch using `mcm/set-theme-options`
4. Tell the user exactly what was configured and why, so they can request specific changes

### For both modes — Critical rules:
- ALWAYS set `general-accent_color_mode` to `color` BEFORE setting the accent color
- ALWAYS set logo via `mcm/set-theme-mod {"key": "custom_logo", "value": <attachment_id>}` — NOT via theme options
- Typography headings require the full array format (see Section 5 below)
- After configuring, tell the user to check the frontend to verify the result

---

## Procedure

### 0) Verify the active theme

Call `mcm/theme-config-guide` — it auto-detects the active theme and confirms it is `dt-the7` (classic theme).

### 1) Read current configuration

IMPORTANT: Always read current options first to understand the existing state. The7 only stores options that differ from defaults — a fresh install may show very few keys.

```json
// Read ALL The7 theme options
mcm/get-theme-options {}

// Read specific options only
mcm/get-theme-options {
  "keys": [
    "general-layout",
    "general-content_width",
    "general-accent_bg_color",
    "footer-style",
    "sidebar-width"
  ]
}

// Read theme mods (logo, menus)
mcm/get-theme-mod {}
```

### 2) Set up site identity

```json
mcm/set-option {"name": "blogname", "value": "Site Name"}
mcm/set-option {"name": "blogdescription", "value": "Site Tagline"}
mcm/set-option {"name": "show_on_front", "value": "page"}
mcm/set-option {"name": "page_on_front", "value": <page_id>}
mcm/set-option {"name": "page_for_posts", "value": <page_id>}
```

### 3) Upload and set the logo (CRITICAL)

The7 uses WordPress standard `custom_logo` theme mod for the site logo. This stores an **attachment ID**, not a URL.

**Step A: Upload the logo image**
```json
mcm/upload-media {"url": "https://example.com/logo.png", "title": "Site Logo"}
// Response includes: attachment_id (e.g., 42) and url
```

**Step B: Set the logo as custom_logo theme mod**
```json
mcm/set-theme-mod {"key": "custom_logo", "value": 42}
// Replace 42 with the actual attachment_id from Step A
```

**Step C: Set the site icon (favicon) as WordPress theme mod**
```json
// Upload the favicon first
mcm/upload-media {"url": "https://example.com/favicon.png", "title": "Favicon"}
// Then set it as site icon
mcm/set-option {"name": "site_icon", "value": <favicon_attachment_id>}
```

**Step D (optional): Set The7 theme-option favicons for retina/device support**
```json
mcm/set-theme-options {
  "values": {
    "general-favicon": "https://example.com/wp-content/uploads/favicon.png",
    "general-favicon_hd": "https://example.com/wp-content/uploads/favicon@2x.png"
  }
}
```

> **Common mistake**: Setting `header-logo-padding` (logo padding) instead of the actual logo image. The padding option only controls spacing AROUND the logo — it does NOT set the logo image itself. The logo image MUST be set via `mcm/set-theme-mod {"key": "custom_logo", "value": <attachment_id>}`.

### 4) Set colors (correct order matters)

**ALWAYS set `general-accent_color_mode` BEFORE setting the accent color value.**

```json
// Step 1: Set accent color mode
mcm/set-theme-options {"values": {"general-accent_color_mode": "color"}}

// Step 2: Set ALL colors together
mcm/set-theme-options {
  "values": {
    "general-accent_bg_color": "#E94560",
    "general-bg_color": "#FFFFFF",
    "general-content_boxes_bg_color": "#FFFFFF",
    "content-headers_color": "#252525",
    "content-primary_text_color": "#686868",
    "content-secondary_text_color": "#999999",
    "content-links_color": "#E94560",
    "dividers-color": "#E8E8E8"
  }
}
```

### 5) Set typography

Typography options use different formats depending on the field type:

**Font family** (string):
```json
mcm/set-theme-options {
  "values": {
    "fonts-font_family": "Open Sans",
    "fonts-headers-font-family": "Montserrat"
  }
}
```

**Heading typography** — each heading uses a structured array with responsive support:
```json
mcm/set-theme-options {
  "values": {
    "fonts-h1-typography": {
      "font_family": "Montserrat",
      "responsive_font_size": {"desktop": "44px"},
      "responsive_line_height": {"desktop": "50px"},
      "text_transform": "none"
    },
    "fonts-h2-typography": {
      "font_family": "Montserrat",
      "responsive_font_size": {"desktop": "26px"},
      "responsive_line_height": {"desktop": "30px"},
      "text_transform": "none"
    },
    "fonts-h3-typography": {
      "font_family": "Montserrat",
      "responsive_font_size": {"desktop": "22px"},
      "responsive_line_height": {"desktop": "30px"},
      "text_transform": "none"
    }
  }
}
```

> **IMPORTANT**: Typography fields are arrays, NOT simple strings. Each heading (`fonts-h1-typography` through `fonts-h6-typography`) requires `font_family`, `responsive_font_size`, `responsive_line_height`, and `text_transform`. Add a `"tablet"` key inside `responsive_font_size`/`responsive_line_height` for responsive sizing. Defaults: H1=44px/50px, H2=26px/30px, H3=22px/30px, H4=18px/20px, H5=15px/20px, H6=12px/20px (font-size/line-height).

### 6) Set layout

```json
mcm/set-theme-options {
  "values": {
    "general-layout": "wide",
    "general-content_width": "1200",
    "general-border_radius": "8",
    "general-page_content_margin": "50px 50px 50px 50px"
  }
}
```

### 7) Configure header

**Step 1: Set header layout type** (8 options, default: `classic`):
```json
mcm/set-theme-options {
  "values": {
    "header-layout": "classic"
  }
}
```
Valid values: `disabled`, `classic`, `inline`, `split`, `side`, `top_line`, `side_line`, `menu_icon`.

**Step 2: Set header background style** (3 options, default: `normal`):
```json
mcm/set-theme-options {
  "values": {
    "header-background": "normal",
    "header-transparent_bg_color": "rgba(0,0,0,0.5)"
  }
}
```
Valid values: `normal`, `overlap`, `transparent`. The `header-transparent_bg_color` only applies when set to `transparent`.

**Step 3: Set per-layout options** (each layout has its own sub-options following the pattern `header-{layout}-*`):
```json
mcm/set-theme-options {
  "values": {
    "header-classic-height": "100px",
    "header-classic-menu-position": "left",
    "header-classic-logo-position": "left",
    "header-classic-is_fullwidth": "0",
    "header-classic-side-padding": "30px 30px"
  }
}
```
Menu position values: `left`, `center`, `justify`. Logo position values: `left`, `center`. Other layouts follow the same pattern (e.g., `header-inline-height`, `header-split-height`).

**Step 4: Set header appearance and menu colors**:
```json
mcm/set-theme-options {
  "values": {
    "header-bg-color": "#ffffff",
    "header-decoration": "shadow",
    "header-menu-font-color": "#333333",
    "header-menu-hover-font-color-style": "accent"
  }
}
```
Header decoration values: `disabled`, `shadow`, `content-width-line`, `line`. Menu hover style: `accent` (inherits accent color), `color` (custom), `gradient`. See [theme-options.md](references/theme-options.md) for the full list of header appearance and menu options.

### 8) Configure footer layout

The7 supports flexible footer column layouts:

```json
mcm/set-theme-options {
  "values": {
    "footer-style": "solid_background",
    "footer-bg_color": "#1B1B1B",
    "footer-layout": "1/4+1/4+1/4+1/4",
    "footer-headers_color": "#ffffff",
    "footer-primary_text_color": "#828282",
    "footer-padding": "50px 50px 50px 50px",
    "bottom_bar-enabled": "1",
    "bottom_bar-copyrights": "Copyright 2026 Your Company"
  }
}
```

### 9) Configure page titles and breadcrumbs

```json
mcm/set-theme-options {
  "values": {
    "general-show_titles": "1",
    "general-title_align": "left",
    "general-title_height": "170px",
    "general-title_bg_mode": "content_line",
    "general-title_bg_color": "#ffffff",
    "general-title_color": "#222222",
    "general-show_breadcrumbs": "1",
    "general-breadcrumbs_color": "#999999"
  }
}
```

### 10) Configure blog settings

```json
mcm/set-theme-options {
  "values": {
    "general-blog_meta_on": "1",
    "general-blog_meta_date": "1",
    "general-blog_meta_author": "1",
    "general-blog_meta_categories": "1",
    "general-blog_meta_comments": "1",
    "general-show_rel_posts": "1",
    "general-rel_posts_max": "3"
  }
}
```

### 11) Configure buttons

```json
mcm/set-theme-options {
  "values": {
    "buttons-color_mode": "accent",
    "buttons-text_color_mode": "color",
    "buttons-text_color": "#ffffff",
    "buttons-hover_color_mode": "accent",
    "buttons-text_hover_color_mode": "color",
    "buttons-text_hover_color": "#ffffff"
  }
}
```

### 12) Configure mobile header

```json
mcm/set-theme-options {
  "values": {
    "header-mobile-first_switch": "1024px",
    "header-mobile-first_switch-height": "80",
    "header-mobile-first_switch-layout": "left_right",
    "header-mobile-second_switch": "760px",
    "header-mobile-second_switch-height": "60",
    "header-mobile-second_switch-layout": "left_right",
    "header-mobile-menu-bg-color": "#111111",
    "header-mobile-menu-font-color": "#ffffff",
    "header-mobile-menu-align": "left",
    "header-mobile-menu-show_dividers": "1"
  }
}
```

### 13) Configure floating header

```json
mcm/set-theme-options {
  "values": {
    "header-show_floating_navigation": "1",
    "header-floating_navigation-height": "80px",
    "header-floating_navigation-bg-color": "rgba(255,255,255,0.95)",
    "header-floating_navigation-decoration": "shadow"
  }
}
```

### 14) Configure top bar (optional)

```json
mcm/set-theme-options {
  "values": {
    "top-bar-height": "40px",
    "top_bar-padding": "0px 50px 0px 50px",
    "top_bar-bg-color": "#333333",
    "top_bar-bg-style": "full_width"
  }
}
```

### 15) Configure social / share buttons

```json
mcm/set-theme-options {
  "values": {
    "social_buttons-visibility": "on_hover",
    "social_buttons-post-button_title": "Share This Post"
  }
}
```

### 16) Configure advanced settings

```json
mcm/set-theme-options {
  "values": {
    "general-images_lazy_loading": "1",
    "general-smooth_scroll": "on",
    "general-responsive": "1",
    "the7_opengraph_tags": "1"
  }
}
```

### 17) Clear caches

The `mcm/set-theme-options` ability automatically clears The7's compiled CSS transients and dynamic CSS cache after updating. No manual cache clearing is needed.

## Important: The7 Color System

The7 uses an **accent color** system with color mode switching:
- `general-accent_color_mode`: `color` or `gradient`
- When set to `color`: uses `general-accent_bg_color` (single hex value)
- When set to `gradient`: uses `general-accent_bg_color_gradient` (gradient definition)

Many options reference the accent color mode. Buttons, image hovers, and other elements can be set to `accent` mode (inherits global accent) or `color` mode (custom color).

**CRITICAL**: Always set `general-accent_color_mode` BEFORE setting the accent color value. If you set the color but not the mode, The7 may use gradient mode and ignore your hex color.

## Important: The7 Logo System

The7 uses **WordPress standard `custom_logo` theme mod** for the site logo:

| What | How | Ability |
|------|-----|---------|
| Site logo | `custom_logo` = attachment ID | `mcm/set-theme-mod` |
| Site icon (favicon) | `site_icon` = attachment ID | `mcm/set-option` |
| The7 favicon | `general-favicon` = URL | `mcm/set-theme-options` |
| The7 retina favicon | `general-favicon_hd` = URL | `mcm/set-theme-options` |
| Logo padding | `header-logo-padding` = spacing | `mcm/set-theme-options` |
| Transparent header logo | `header-style-transparent-choose_logo` = `custom`/`main`/`none` | `mcm/set-theme-options` |
| Floating header logo | `header-style-floating-choose_logo` = `custom`/`main`/`none` | `mcm/set-theme-options` |
| Mobile logo mode | `header-mobile-first_switch-logo` = `desktop`/`mobile` | `mcm/set-theme-options` |

The `-choose_logo` radio options let each header variant use the MAIN logo (`main`), a CUSTOM logo (`custom`), or hide the logo entirely (`none`). The mobile logo option uses `desktop` (inherit desktop logo) or `mobile` (use custom mobile logo).

## Minimum Configuration Checklist

At minimum, when setting up The7 from scratch, set ALL of these:

**Required (theme mods via `mcm/set-theme-mod`):**
- [ ] `custom_logo` — Site logo (attachment ID)

**Required (WP options via `mcm/set-option`):**
- [ ] `blogname` — Site name
- [ ] `blogdescription` — Tagline
- [ ] `site_icon` — Favicon (attachment ID)
- [ ] `show_on_front` — `page` for static homepage
- [ ] `page_on_front` — Homepage page ID
- [ ] `page_for_posts` — Blog page ID

**Required (theme options via `mcm/set-theme-options`):**
- [ ] `general-accent_color_mode` — Set to `color`
- [ ] `general-accent_bg_color` — Primary accent color
- [ ] `general-bg_color` — Body background
- [ ] `content-headers_color` — Heading text color
- [ ] `content-primary_text_color` — Body text color
- [ ] `fonts-font_family` — Body font
- [ ] `fonts-headers-font-family` — Heading font
- [ ] `footer-style` — Footer style
- [ ] `footer-bg_color` — Footer background
- [ ] `footer-headers_color` — Footer heading color
- [ ] `footer-primary_text_color` — Footer text color
- [ ] `footer-layout` — Footer columns
- [ ] `bottom_bar-copyrights` — Copyright text

**Recommended (theme options via `mcm/set-theme-options`):**
- [ ] `general-layout` — `wide` or `boxed`
- [ ] `general-content_width` — Content width in px
- [ ] `general-border_radius` — Global border radius
- [ ] `content-links_color` — Link color
- [ ] `content-secondary_text_color` — Secondary text color
- [ ] `general-content_boxes_bg_color` — Content boxes background
- [ ] `dividers-color` — Divider color
- [ ] `general-show_titles` — Show page titles
- [ ] `general-show_breadcrumbs` — Show breadcrumbs
- [ ] `buttons-color_mode` — Button color mode
- [ ] `buttons-text_color` — Button text color
- [ ] `header-show_floating_navigation` — Floating header
- [ ] `header-mobile-first_switch` — Tablet breakpoint
- [ ] `header-mobile-second_switch` — Phone breakpoint
- [ ] `header-mobile-menu-bg-color` — Mobile menu background
- [ ] `general-images_lazy_loading` — Lazy loading
- [ ] `general-smooth_scroll` — Smooth scroll
- [ ] `social_buttons-visibility` — Share buttons visibility

## Verification

After configuring, verify each area:

- [ ] Logo displays in the header (check desktop and mobile)
- [ ] Colors display correctly (accent, background, text, headers)
- [ ] Typography (body, headings H1-H6) renders correctly
- [ ] Header layout and styling are correct
- [ ] Mobile header switches at correct breakpoints
- [ ] Floating header appears on scroll with correct styling
- [ ] Top bar displays correctly (if enabled)
- [ ] Micro-widgets show in correct header positions (if configured)
- [ ] Footer style, colors, and columns are correct
- [ ] Bottom bar with copyright displays correctly
- [ ] Page titles and breadcrumbs display correctly
- [ ] Responsive titles work on mobile (if enabled)
- [ ] Blog layout and meta display correctly
- [ ] Social share buttons appear on posts (if enabled)
- [ ] Button styles are correct (all 5 sizes if used)
- [ ] Sidebar width and style are correct
- [ ] Image hover effects work correctly
- [ ] Loading animation works (if enabled)
- [ ] Lazy loading is functioning (if enabled)
- [ ] Dynamic CSS has been regenerated (automatic)

## Failure modes / debugging

- **Logo not showing:** Check that `custom_logo` theme mod is set to a valid attachment ID (not a URL). Use `mcm/get-theme-mod {"key": "custom_logo"}` to verify. Common mistake: trying to set the logo via `mcm/set-theme-options` — logo is a theme mod, not a theme option.
- **Colors not applying:** Verify `general-accent_color_mode` is set to `color` before setting `general-accent_bg_color`. If set to `gradient`, the hex color value is ignored.
- **Changes not visible:** The MCP ability auto-clears The7's compiled CSS transients; clear browser cache if needed.
- **Option not saving:** The `mcm/set-theme-options` ability reads the full `the7` array before updating — it merges only the keys you specify.
- **Few options in `the7`:** This is normal — The7 only stores options that differ from defaults. A fresh install may have very few keys. All ~200 options from the reference file ARE available but use built-in defaults until explicitly set.
- **Spacing options:** Use format `"50px 50px 50px 50px"` (top right bottom left).
- **Footer layout:** Uses string format like `"1/4+1/4+1/4+1/4"` or `"1/3+1/3+1/3"`.
- **Typography format:** Heading typography fields (`fonts-h1-typography` through `fonts-h6-typography`) require a structured array with `font_family`, `responsive_font_size` (object with `desktop` and optional `tablet` keys), `responsive_line_height`, and `text_transform`. Passing a simple string like `"44px"` will NOT work.
- **Discovering all available option keys:** Run `mcm/get-theme-options {}` to see currently set keys. For the full list of available options, see the [theme-options.md](references/theme-options.md) reference file.
- **Loading animation not changing:** Check `general-beautiful_loading` option (values: `enabled`, `disabled`).

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all option IDs with types and defaults
- **[../global-styles-api.md](../global-styles-api.md)** — Shared reference (see Section 0 for Classic vs FSE differences)
