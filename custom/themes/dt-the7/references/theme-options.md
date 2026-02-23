# The7 — Configurable Options

The7 uses **two storage mechanisms** for configuration:

1. **Theme options** (`the7mk2` in `wp_options`): All visual styling options. Read via `mcm/get-theme-options` and update via `mcm/set-theme-options` (auto-detects `the7mk2` for The7).
2. **Theme mods** (`theme_mods_dt-the7` in `wp_options`): Logo and menu locations. Read via `mcm/get-theme-mod` and update via `mcm/set-theme-mod`.

> **IMPORTANT**: The7 only stores options in `the7mk2` when they differ from defaults. A fresh install may have very few keys. All options listed below ARE available — they use built-in defaults until explicitly set.

---

## Logo & Site Identity (Theme Mods + WP Options)

**These are NOT stored in `the7mk2`.** They use WordPress standard APIs:

| Setting | Storage | How to Set | Value Type |
|---------|---------|------------|------------|
| **Site logo** | Theme mod `custom_logo` | `mcm/set-theme-mod {"key": "custom_logo", "value": <attachment_id>}` | Integer (attachment ID) |
| Site icon (favicon) | WP option `site_icon` | `mcm/set-option {"name": "site_icon", "value": <attachment_id>}` | Integer (attachment ID) |
| Site name | WP option `blogname` | `mcm/set-option {"name": "blogname", "value": "Name"}` | String |
| Site tagline | WP option `blogdescription` | `mcm/set-option {"name": "blogdescription", "value": "Tagline"}` | String |
| Static homepage | WP option `show_on_front` | `mcm/set-option {"name": "show_on_front", "value": "page"}` | String |
| Homepage page | WP option `page_on_front` | `mcm/set-option {"name": "page_on_front", "value": <page_id>}` | Integer |
| Blog page | WP option `page_for_posts` | `mcm/set-option {"name": "page_for_posts", "value": <page_id>}` | Integer |
| Menu locations | Theme mod `nav_menu_locations` | `mcm/update-menu {"action": "assign_location", ...}` | Object |

### Logo Setup Procedure

```
1. mcm/upload-media {"url": "https://example.com/logo.png", "title": "Site Logo"}
   → Returns: {"attachment_id": 42, "url": "https://..."}

2. mcm/set-theme-mod {"key": "custom_logo", "value": 42}
   → Logo now displays in the header
```

> **Common mistake**: Setting `header-logo-padding` thinking it's the logo image. That option only controls spacing AROUND the logo. The actual logo image MUST be set via `custom_logo` theme mod.

---

## Branding Options (Theme Options in `the7mk2`)

These control logo padding, favicon URLs, and logo variant selection per header mode:

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-logo-padding` | spacing | `0px 0px 0px 0px` | Main logo padding |
| `header-style-transparent-choose_logo` | radio | `custom` | Transparent header logo source (`custom`, `main`, or `none`) |
| `header-style-transparent-logo-padding` | spacing | `0px` all | Transparent logo padding |
| `header-style-floating-choose_logo` | radio | `custom` | Floating header logo source (`custom`, `main`, or `none`) |
| `header-style-floating-logo-padding` | spacing | `0px` all | Floating logo padding |
| `header-mobile-first_switch-logo` | radio | `mobile` | Mobile logo 1st breakpoint — `desktop` (use desktop logo) or `mobile` (use custom mobile logo) |
| `header-mobile-second_switch-logo` | radio | `mobile` | Mobile logo 2nd breakpoint — `desktop` (use desktop logo) or `mobile` (use custom mobile logo) |
| `header-style-mobile-logo-padding` | spacing | `0px` all | Mobile logo padding |
| `header-style-mixed-logo-padding` | spacing | `0px` all | Mixed header logo padding |
| `header-style-mixed-transparent-top_line-choose_logo` | radio | `main` | Mixed transparent top-line logo: `custom`, `main`, `none` |
| `header-style-mixed-top_line-floating-choose_logo` | radio | `main` | Mixed top-line floating logo: `custom`, `main`, `none` |
| `header-transparent-mobile-first_switch-logo` | radio | `desktop` | Transparent header mobile 1st: `desktop`, `mobile` |
| `header-transparent-mobile-second_switch-logo` | radio | `desktop` | Transparent header mobile 2nd: `desktop`, `mobile` |
| `header-floating-mobile-first_switch-logo` | radio | `desktop` | Floating header mobile 1st: `desktop`, `mobile` |
| `header-floating-mobile-second_switch-logo` | radio | `desktop` | Floating header mobile 2nd: `desktop`, `mobile` |
| `header-style-transparent-mobile-logo-padding` | spacing | `0px` all | Transparent mobile logo padding |
| `header-style-floating-mobile-logo-padding` | spacing | `0px` all | Floating mobile logo padding |
| `bottom_bar-logo-padding` | spacing | `0px` all | Bottom bar logo padding |
| `general-favicon` | upload | — | Favicon URL (The7-specific) |
| `general-favicon_hd` | upload | — | Retina favicon URL |
| `general-handheld_icon-old_iphone` | upload | — | iPhone icon |
| `general-handheld_icon-old_ipad` | upload | — | iPad icon |
| `general-handheld_icon-retina_iphone` | upload | — | Retina iPhone icon |
| `general-handheld_icon-retina_ipad` | upload | — | Retina iPad icon |

The `-choose_logo` radio options control which logo each header variant uses:
- `main` = Uses the WordPress `custom_logo` theme mod
- `custom` = Uses a custom logo (configured in admin panel)
- `none` = Don't show logo in this header variant

---

## General / Layout

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-layout` | images | `wide` | Site layout (wide/boxed) |
| `general-content_width` | number | `1200` | Content width (px) |
| `general-box_width` | number | `1320` | Boxed layout width (px) |
| `general-page_content_margin` | spacing | `50px 50px 50px 50px` | Content margin |
| `general-switch_content_paddings` | number | `778` | Mobile padding breakpoint |
| `general-page_content_mobile_margin` | spacing | `50px 20px 50px 20px` | Mobile content margin |
| `general-border_radius` | number | `8` | Global border radius (px) |

---

## Colors

**CRITICAL**: Always set `general-accent_color_mode` to `color` BEFORE setting `general-accent_bg_color`. If the mode is `gradient`, The7 ignores the hex color.

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-accent_color_mode` | radio | `color` | Accent mode (`color` or `gradient`) — SET THIS FIRST |
| `general-accent_bg_color` | color | `#D73B37` | Accent color (only used when mode is `color`) |
| `general-accent_bg_color_gradient` | gradient | `45deg\|...` | Accent gradient (only used when mode is `gradient`) |
| `general-bg_color` | alpha_color | `#252525` | Body background color |
| `general-bg_image` | background_img | — | Body background image |
| `general-bg_fullscreen` | checkbox | `0` | Fullscreen body bg |
| `general-bg_fixed` | checkbox | `0` | Fixed body bg |
| `general-boxed_bg_color` | color | `#ffffff` | Boxed layout bg color |
| `general-boxed_bg_image` | background_img | — | Boxed layout bg image |
| `general-content_boxes_bg_color` | alpha_color | `#FFFFFF` | Content boxes bg |
| `general-content_boxes_decoration` | images | `none` | Content box decoration |
| `general-content_boxes_decoration_outline_color` | alpha_color | `#FFFFFF` | Box outline color |
| `dividers-color` | alpha_color | `#cccccc` | Divider color |

### Content Colors

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `content-headers_color` | color | `#252525` | Heading text color |
| `content-primary_text_color` | color | `#686868` | Primary text color |
| `content-secondary_text_color` | color | `#999999` | Secondary text color |
| `content-links_color` | color | `#999999` | Link color |

### Complete Color Setup Example

```json
mcm/set-theme-options {
  "values": {
    "general-accent_color_mode": "color",
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

---

## Typography / Fonts

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `fonts-font_family` | web_fonts | `Arial` | Body font family (e.g., `Open Sans`, `Roboto`) |
| `fonts-big_size` | font_sizes | — | Large text sizes |
| `fonts-normal_size` | font_sizes | — | Normal text sizes |
| `fonts-small_size` | font_sizes | — | Small text sizes |
| `fonts-headers-font-family` | web_fonts | — | Heading font family (e.g., `Montserrat`) |
| `fonts-headers-text-transform` | select | — | Heading text transform (`none`, `uppercase`, `lowercase`, `capitalize`) |
| `fonts-h1-typography` | typography | array (see below) | H1 typography — default: 44px/50px |
| `fonts-h2-typography` | typography | array (see below) | H2 typography — default: 26px/30px |
| `fonts-h3-typography` | typography | array (see below) | H3 typography — default: 22px/30px |
| `fonts-h4-typography` | typography | array (see below) | H4 typography — default: 18px/20px |
| `fonts-h5-typography` | typography | array (see below) | H5 typography — default: 15px/20px |
| `fonts-h6-typography` | typography | array (see below) | H6 typography — default: 12px/20px |
| `fonts-widget-title` | typography | array (see below) | Widget title typography — default: 15px/20px |
| `fonts-widget-content` | typography | array (see below) | Widget content typography — default: 13px/20px |
| `widget_gap` | number | `15px` | Widget gap/spacing |

### Typography Format

**IMPORTANT**: Heading typography fields are **structured arrays**, NOT simple strings. Passing `"44px"` will NOT work.

Each typography field requires this structure:
```json
{
  "font_family": "Montserrat",
  "responsive_font_size": {
    "desktop": "44px",
    "tablet": "32px"
  },
  "responsive_line_height": {
    "desktop": "50px",
    "tablet": "38px"
  },
  "text_transform": "none"
}
```

- `font_family`: Google Font name or system font (e.g., `"Open Sans"`, `"Arial"`)
- `responsive_font_size`: Object with `"desktop"` key (required) and optional `"tablet"` key
- `responsive_line_height`: Same structure as font_size
- `text_transform`: `"none"`, `"uppercase"`, `"lowercase"`, or `"capitalize"`

For **font family** (`fonts-font_family`, `fonts-headers-font-family`), pass the Google Font name as a simple string: `"Open Sans"`, `"Montserrat"`.

### Typography Setup Example

```json
mcm/set-theme-options {
  "values": {
    "fonts-font_family": "Open Sans",
    "fonts-headers-font-family": "Montserrat",
    "fonts-headers-text-transform": "none",
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
    },
    "fonts-h4-typography": {
      "font_family": "Montserrat",
      "responsive_font_size": {"desktop": "18px"},
      "responsive_line_height": {"desktop": "20px"},
      "text_transform": "none"
    },
    "fonts-h5-typography": {
      "font_family": "Montserrat",
      "responsive_font_size": {"desktop": "15px"},
      "responsive_line_height": {"desktop": "20px"},
      "text_transform": "none"
    },
    "fonts-h6-typography": {
      "font_family": "Montserrat",
      "responsive_font_size": {"desktop": "12px"},
      "responsive_line_height": {"desktop": "20px"},
      "text_transform": "none"
    }
  }
}
```

> **Tip**: To see the current format on a specific site, read a typography key with `mcm/get-theme-options {"keys": ["fonts-h1-typography"]}` and match its structure when updating.

---

## Header

### Header Layout

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-layout` | images | `classic` | Header layout type: `disabled`, `classic`, `inline`, `split`, `side`, `top_line`, `side_line`, `menu_icon` |
| `header-background` | images | `normal` | Header bg style: `normal`, `overlap`, `transparent` |
| `header-transparent_bg_color` | alpha_color | `rgba(0,0,0,0.5)` | Transparent header bg color (only when `header-background` = `transparent`) |
| `top-bar-transparent_bg_color` | alpha_color | `rgba(0,0,0,0.5)` | Transparent top bar bg color |

### Per-Layout Options

Each header layout has its own sub-options following the pattern `header-{layout}-*`. The most common layout is `classic`:

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-classic-height` | number | `140px` | Header height |
| `header-classic-side-padding` | spacing | `30px 30px` | Header left/right padding |
| `header-classic-menu-position` | images | `left` | Menu position: `left`, `center`, `justify` |
| `header-classic-menu-margin` | spacing | `0px 0px` | Menu top/bottom margin |
| `header-classic-logo-position` | images | `left` | Logo position: `left`, `center` |
| `header-classic-is_fullwidth` | images | `0` | Full-width header: `1` (enabled), `0` (disabled) |

Other layouts follow the same pattern: `header-inline-height`, `header-split-height`, `header-side-height`, etc. Use `mcm/get-theme-options {}` to discover all header-related keys on a specific installation.

### Header Appearance

Global header styling options (independent of layout type):

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-bg-color` | alpha_color | `#000000` | Header background color |
| `header-bg-image` | background_img | — | Header background image |
| `header-bg-is_fullscreen` | checkbox | `0` | Fullscreen header background |
| `header-bg-is_fixed` | checkbox | `0` | Fixed header background |
| `header-decoration` | images | `shadow` | Header bottom decoration: `disabled`, `shadow`, `content-width-line`, `line` |
| `header-decoration-color` | alpha_color | `#ffffff` | Header decoration color |
| `header-decoration-line_size` | number | `1px` | Decoration line size |

### Header Menu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-menu-typography` | typography | array | Menu font typography (same array format as headings) |
| `header-menu-icon-size` | slider | `16` | Menu icon size (px) |
| `header-menu-show_next_lvl_icons` | checkbox | `1` | Show submenu dropdown arrows |
| `header-menu-submenu-parent_is_clickable` | checkbox | `1` | Parent menu items are clickable |
| `header-menu-submenu-display` | radio | `hover` | Submenu display trigger: `hover`, `click` |
| `header-menu-subtitle-typography` | typography | array | Menu subtitle font |
| `header-menu-font-color` | color | `#ffffff` | Menu font color |
| `header-menu-hover-font-color-style` | radio | `accent` | Menu hover color mode: `accent`, `color`, `gradient` |
| `header-menu-hover-font-color` | color | `#ffffff` | Menu hover color (when style = `color`) |
| `header-menu-hover-font-gradient` | gradient | — | Menu hover gradient (when style = `gradient`) |

---

## Footer

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `footer-style` | images | `content_width_line` | Footer style: `content_width_line`, `full_width_line`, `solid_background` |
| `footer-bg_color` | alpha_color | `#1B1B1B` | Footer background |
| `footer-decoration` | images | `none` | Footer decoration |
| `footer-decoration_outline_color` | alpha_color | `#FFFFFF` | Decoration outline |
| `footer-decoration-line_size` | number | `1px` | Decoration line size |
| `footer-bg_image` | background_img | — | Footer bg image |
| `footer-slide-out-mode` | images | `0` | Slide-out footer mode |
| `footer-headers_color` | color | `#ffffff` | Footer heading color |
| `footer-primary_text_color` | color | `#828282` | Footer text color |
| `footer-accent_text_color` | color | — | Footer accent color |
| `footer-padding` | spacing | `50px 50px 50px 50px` | Footer padding |
| `footer-collapse_after` | number | `760px` | Footer collapse breakpoint |
| `footer-mobile_padding` | spacing | `50px 20px 50px 20px` | Mobile footer padding |
| `footer-collapse_columns_after` | number | `760px` | Column collapse breakpoint |
| `footer-paddings-columns` | number | `44px` | Column padding |
| `footer-layout` | text | `1/4+1/4+1/4+1/4` | Column layout |
| `footer-is_fullwidth` | images | `0` | Full-width footer |

### Bottom Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `bottom_bar-enabled` | radio | `1` | Enable bottom bar |
| `bottom_bar-style` | images | `content_width_line` | Bottom bar style |
| `bottom_bar-bg_color` | alpha_color | `#ffffff` | Bottom bar bg |
| `bottom_bar-line_size` | number | `1px` | Bottom bar line size |
| `bottom_bar-bg_image` | background_img | — | Bottom bar bg image |
| `bottom_bar-layout` | images | `logo_left` | Bottom bar layout |
| `bottom_bar-height` | number | `60px` | Bottom bar height |
| `bottom_bar-padding` | spacing | `10 10` | Bottom bar padding |
| `bottom_bar-collapse_after` | number | `990px` | Collapse breakpoint |
| `bottom_bar-color` | color | `#757575` | Bottom bar text color |
| `bottom_bar-text` | textarea | — | Bottom bar custom text |
| `bottom_bar-copyrights` | textarea | — | Copyright text |
| `bottom_bar-credits` | checkbox | `1` | Show theme credits |
| `bottom_bar-logo-padding` | spacing | `0px` all | Bottom bar logo padding |

### Footer Setup Example

```json
mcm/set-theme-options {
  "values": {
    "footer-style": "solid_background",
    "footer-bg_color": "#1B1B1B",
    "footer-layout": "1/3+1/3+1/3",
    "footer-headers_color": "#ffffff",
    "footer-primary_text_color": "#828282",
    "footer-padding": "50px 50px 50px 50px",
    "bottom_bar-enabled": "1",
    "bottom_bar-copyrights": "© 2026 Your Company. All rights reserved."
  }
}
```

---

## Page Titles & Breadcrumbs

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-show_titles` | images | `1` | Show page titles |
| `general-title_align` | images | `left` | Title alignment |
| `general-title_height` | number | `170px` | Title area height |
| `page_title-padding` | spacing | `0px 0px` | Title padding |
| `general-title_bg_mode` | images | `content_line` | Title bg mode |
| `general-title_bg_color` | alpha_color | `#ffffff` | Title bg color |
| `general-title_enable_bg_img` | radio | `disabled` | Enable title bg image |
| `general-title_bg_image` | background_img | — | Title bg image |
| `general-title_bg_fullscreen` | checkbox | `0` | Fullscreen title bg |
| `general-title_bg_overlay` | checkbox | `0` | Title bg overlay |
| `general-title_overlay_color` | alpha_color | `rgba(0,0,0,0.5)` | Overlay color |
| `general-title_scroll_effect` | radio | `default` | Scroll effect |
| `general-title_bg_parallax` | text | `0.5` | Parallax speed |
| `general-page-title-typography` | typography | — | Title typography |
| `general-title_color` | color | `#222222` | Title text color |
| `general-title_decoration` | radio | `none` | Title decoration: `none`, `outline` |
| `general-title_decoration_outline_color` | alpha_color | `#FFFFFF` | Title decoration outline color |
| `general-title_decoration_outline_height` | number | `1px` | Title decoration outline height |
| `general-title_decoration_outline_style` | select | `solid` | `solid`, `dotted`, `dashed`, `double` |
| `general-title_decoration_line_color` | alpha_color | `rgba(51,51,51,0.11)` | Content-line decoration color |
| `general-title_decoration_line_height` | number | `1px` | Content-line decoration height |
| `general-title_decoration_line_style` | select | `solid` | `solid`, `dotted`, `dashed`, `double` |
| `general-title_bg_gradient` | gradient | — | Title area gradient (when bg_mode = `gradient`) |
| `page_title-background-style-transparent-color_scheme` | radio | `from_options` | Transparent header color scheme: `from_options`, `light` |
| `general-show_breadcrumbs` | images | `1` | Show breadcrumbs |
| `breadcrumbs-typography` | typography | — | Breadcrumb typography |
| `general-breadcrumbs_color` | color | `#ffffff` | Breadcrumb color |
| `breadcrumbs_padding` | spacing | `3px 12px 2px 12px` | Breadcrumb padding |
| `breadcrumbs_margin` | spacing | `0px` all | Breadcrumb margin |
| `general-breadcrumbs_bg_color` | images | `disabled` | Enable breadcrumb background: `enabled`, `disabled` |
| `breadcrumbs_bg_color` | alpha_color | `rgba(255,255,255,0.2)` | Breadcrumb bg color (only when `general-breadcrumbs_bg_color` = `enabled`) |
| `breadcrumbs_border_radius` | number | `2px` | Breadcrumb border radius |
| `breadcrumbs_border_width` | number | `0px` | Breadcrumb border width |
| `breadcrumbs_border_color` | alpha_color | `rgba(255,255,255,0.5)` | Breadcrumb border color |

### Responsive Title

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-titles_responsiveness` | radio | `0` | Enable responsive titles |
| `general-titles-responsiveness-switch` | number | `990px` | Responsive breakpoint |
| `general-responsive_title_height` | number | `150px` | Mobile title height |
| `general-responsive_title_size` | slider | `20` | Mobile title size |
| `general-responsive_title_line_height` | slider | `30` | Mobile line height |
| `general-title_responsive_breadcrumbs` | checkbox | `0` | Mobile breadcrumbs |

---

## Blog & Portfolio

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-filter_style` | images | `ios` | Filter style |
| `general-filter_style-minimal-border_radius` | number | `100px` | Minimal filter radius |
| `general-filter_style-material-line_size` | number | `2px` | Material filter line |
| `filter-typography` | typography | — | Filter typography |
| `general-filter-padding` | spacing | `5px 5px 5px 5px` | Filter padding |
| `general-filter-margin` | spacing | `0px 5px 0px 5px` | Filter margin |
| `general-navigation_margin` | number | `50px` | Navigation margin |
| `blog-fancy_date-style` | images | `circle` | Fancy date style |
| `post-show_fancy_date` | checkbox | `1` | Show fancy date |
| `post-show_fancy_categories` | checkbox | `1` | Show fancy categories |
| `blog-thumbnail_size` | radio | `original` | Thumbnail size mode |
| `blog-thumbnail_proportions` | square_size | — | Thumbnail proportions |
| `general-show_author_in_blog` | images | `1` | Show author in blog |
| `general-next_prev_in_blog` | images | `1` | Previous/next navigation |
| `general-show_back_button_in_post` | images | `0` | Show back button |
| `general-post_back_button_url` | text | — | Back button URL (when show_back_button enabled) |
| `general-blog_meta_on` | images | `1` | Show blog meta |
| `general-blog_meta_date` | checkbox | `1` | Show date |
| `general-blog_meta_author` | checkbox | `1` | Show author |
| `general-blog_meta_categories` | checkbox | `1` | Show categories |
| `general-blog_meta_comments` | checkbox | `1` | Show comments |
| `general-blog_meta_tags` | checkbox | `1` | Show tags |
| `general-show_rel_posts` | images | `0` | Show related posts |
| `general-rel_posts_head_title` | text | — | Related posts title |
| `general-rel_posts_max` | text | `6` | Max related posts |

---

## Buttons

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `buttons-color_mode` | radio | `accent` | Button color mode: `disabled`, `accent`, `color`, `gradient` |
| `buttons-color` | alpha_color | `#ffffff` | Button custom color (when mode is `color`) |
| `buttons-color_gradient` | gradient | — | Button gradient |
| `buttons-hover_color_mode` | radio | `accent` | Hover color mode: `disabled`, `accent`, `color`, `gradient` |
| `buttons-hover_color` | alpha_color | `#ffffff` | Hover custom color |
| `buttons-text_color_mode` | radio | `color` | Text color mode |
| `buttons-text_color` | alpha_color | `#ffffff` | Text color |
| `buttons-text_hover_color_mode` | radio | `color` | Hover text mode |
| `buttons-text_hover_color` | alpha_color | `#ffffff` | Hover text color |
| `buttons-border-color_mode` | radio | `accent` | Border color mode |
| `buttons-border-color` | alpha_color | `#ffffff` | Border color |
| `buttons-hover-border-color_mode` | radio | `accent` | Hover border mode |
| `buttons-hover-border-color` | alpha_color | `#ffffff` | Hover border color |
| `button-shadow` | shadow | — | Button shadow |
| `button-shadow-hover` | shadow | — | Button hover shadow |

### Button Sizes (for each size: s, m, l, lg, xl)

| Pattern | Type | Description |
|---------|------|-------------|
| `buttons-{size}-typography` | typography | Size typography |
| `buttons-{size}-min-width` | slider | Minimum width |
| `buttons-{size}-min-height` | slider | Minimum height |
| `buttons-{size}_padding` | spacing | Button padding |
| `buttons-{size}_border_radius` | number | Border radius |
| `buttons-{size}_border_width` | number | Border width |

---

## Sidebar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `sidebar-width` | number | `30%` | Sidebar width |
| `sidebar-vertical_distance` | number | `60px` | Vertical spacing |
| `sidebar-distance_to_content` | number | `50px` | Distance to content |
| `sidebar-visual_style` | images | `with_dividers` | Sidebar style |
| `sidebar-divider-vertical` | images | `1` | Show vertical divider |
| `sidebar-divider-horizontal` | images | `1` | Show horizontal divider |
| `sidebar-bg_color` | alpha_color | `#ffffff` | Sidebar bg color |
| `sidebar-bg_image` | background_img | — | Sidebar bg image |
| `sidebar-decoration` | images | `none` | Sidebar decoration: `none`, `shadow`, `outline` |
| `sidebar-decoration_outline_color` | alpha_color | `#FFFFFF` | Sidebar outline color (when decoration = `outline`) |
| `sidebar-floating` | checkbox | `0` | Floating sidebar |
| `sidebar-headers_color` | color | `#000000` | Sidebar heading color |
| `sidebar-primary_text_color` | color | `#686868` | Sidebar text color |
| `sidebar-responsiveness` | number | `970px` | Sidebar responsive breakpoint |

---

## Image Hovers

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `image_hover-style` | images | `none` | Hover style |
| `image_hover-color_mode` | radio | `accent` | Hover color mode |
| `image_hover-color` | alpha_color | `#ffffff` | Hover color |
| `image_hover-color_gradient` | gradient | — | Hover gradient |
| `image_hover-opacity` | slider | `30` | Hover opacity (%) |
| `image_hover-project_rollover_color_mode` | radio | `accent` | Portfolio rollover mode |
| `image_hover-project_rollover_color` | alpha_color | `#ffffff` | Portfolio rollover color |
| `image_hover-project_rollover_color_gradient` | gradient | — | Portfolio rollover gradient (when mode = `gradient`) |
| `image_hover-project_rollover_opacity` | slider | `70` | Portfolio rollover opacity |

---

## Loading & Overlay

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-beautiful_loading` | images | `enabled` | Loading animation |
| `general-fullscreen_overlay_color_mode` | radio | `accent` | Overlay color mode |
| `general-fullscreen_overlay_color` | alpha_color | `#ffffff` | Overlay color |
| `general-fullscreen_overlay_gradient` | gradient | — | Overlay gradient |
| `general-fullscreen_overlay_opacity` | slider | `100` | Overlay opacity |
| `general-spinner_color` | alpha_color | `#ffffff` | Spinner color |
| `general-loader_style` | radio | `double_circles` | Loader animation style |
| `general-custom_loader` | textarea | — | Custom loader HTML |
| `general-lightbox_overlay_opacity` | slider | `85` | Lightbox overlay opacity |
| `general-lightbox_arrow_size` | number | `62px` | Lightbox arrow size |

---

## Contact Form

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `input_height` | number | `38px` | Input field height |
| `input_color` | color | `#787d85` | Input text color |
| `input_bg_color` | alpha_color | `#fcfcfc` | Input background |
| `input_border_radius` | number | `0px` | Input border radius |
| `input_border_width` | spacing | `1px 1px 1px 1px` | Input border width |
| `input_border_color` | alpha_color | `rgba(173,176,182,0.3)` | Input border color |
| `input_padding` | spacing | `5px 15px 5px 15px` | Input padding |
| `contact_form_message` | radio | `1` | Show form messages |
| `message_color` | color | `#fff` | Message text color |
| `message_bg_color` | alpha_color | — | Message bg color |
| `general-contact_form_send_mail_to` | text | — | Contact form email |
| `custom_error_messages_validation` | textarea | — | Validation error message text |
| `custom_error_messages` | textarea | — | Send error message text |
| `custom_success_messages` | textarea | — | Success message text |
| `contact_form_security_token` | text | — | Security token |
| `contact_form_recaptcha_site_key` | text | — | reCAPTCHA site key |
| `contact_form_recaptcha_secret_key` | password | — | reCAPTCHA secret key |

---

## Advanced Settings

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-responsive` | radio | `1` | Responsive layout (`1`=enabled, `0`=disabled) |
| `general-images_lazy_loading` | radio | `1` | Images lazy loading (`1`=enabled, `0`=disabled) |
| `general-smooth_scroll` | radio | `on` | Smooth scroll behavior (`on`, `off`, `on_parallax`) |
| `advanced-speed_img_resize` | radio | `1` | Fast image resize engine (`1`=enabled, `0`=disabled) |
| `general-user_scalable` | radio | `0` | Accessibility: allow pinch-to-zoom (`1`=enabled, `0`=disabled) |
| `advanced-fvm_enable_integration` | radio | `1` | Fast Velocity Minify plugin integration (`1`=enabled, `0`=disabled) |
| `advanced-fvm_script_timeout` | number | `50` | Delay loading merged scripts (ms, 50-1000 recommended) |
| `the7_opengraph_tags` | radio | `1` | Enable The7 OpenGraph meta tags (`1`=enabled, `0`=disabled) |
| `general-custom_css` | code_editor | — | Custom CSS code (text/css format) |
| `general-tracking_code` | code_editor | — | Tracking code / Google Analytics / JavaScript |

---

## Mobile Header

### Breakpoints & Layout

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-mobile-first_switch` | number | `1024px` | Tablet breakpoint (1st mobile breakpoint) |
| `header-mobile-first_switch-height` | number | `150` | Header height at tablet breakpoint (px) |
| `header-mobile-first_switch-layout` | images | `left_right` | Tablet layout: `left_right`, `left_center`, `right_left`, `right_center` |
| `header-mobile-second_switch` | number | `760px` | Phone breakpoint (2nd mobile breakpoint) |
| `header-mobile-second_switch-height` | number | `100` | Header height at phone breakpoint (px) |
| `header-mobile-second_switch-layout` | images | `left_right` | Phone layout: `left_right`, `left_center`, `right_left`, `right_center` |

### Mobile Menu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-mobile-menu-typography` | typography | array | Mobile menu font (family, size, transform) |
| `header-mobile-submenu-typography` | typography | array | Mobile submenu font |
| `header-mobile-menu-font-color` | color | `#ffffff` | Mobile menu normal font color |
| `header-mobile-menu-font-hover-color-style` | radio | `accent` | Mobile menu hover mode: `accent`, `color`, `gradient` |
| `header-mobile-menu-font-hover-color` | color | `#ffffff` | Mobile menu hover color (when style=`color`) |
| `header-mobile-menu-font-hover-gradient` | gradient | — | Mobile menu hover gradient (when style=`gradient`) |
| `header-mobile-menu-show_dividers` | images | `1` | Show menu dividers (1=yes, 0=no) |
| `header-mobile-menu-dividers-height` | number | `1px` | Menu divider thickness |
| `header-mobile-menu-dividers-color` | alpha_color | `rgba(153,153,153,0.12)` | Menu divider color |
| `header-mobile-menu-bg-color` | alpha_color | `#111111` | Mobile menu background color |
| `header-mobile-content-padding` | spacing | `45px 15px 30px 30px` | Mobile menu content padding |
| `header-mobile-menu-bg-width` | number | `400px` | Mobile menu max background width |
| `header-mobile-menu-align` | images | `left` | Mobile menu slide direction: `left`, `right` |
| `header-mobile-overlay-bg-color` | alpha_color | `rgba(17,17,17,0.5)` | Website overlay color when menu open |
| `header-mobile-menu-close_icon-position` | radio | `right` | Close button position: `left`, `center`, `right`, `outside` |
| `header-mobile-menu-close_icon-size` | images | `fade_medium` | Close icon style |
| `header-mobile-menu-close_icon-caption` | radio | `disabled` | Close button caption: `disabled`, `left`, `right` |
| `header-mobile-menu-close_icon-caption-text` | text | `Menu` | Close button caption text |
| `header-mobile-menu-close_icon-caption-typography` | typography | array | Close caption font |
| `header-mobile-menu-close_icon-caption_gap` | number | `10px` | Gap between icon and caption |
| `header-mobile-menu_close_icon-bg-border-width` | number | `0px` | Close button border width |
| `header-mobile-menu_close_icon-bg-border-radius` | number | `0px` | Close button border radius |

---

## Floating Header

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-show_floating_navigation` | images | `1` | Enable floating navigation (1=yes, 0=no) |
| `header-floating_navigation-height` | number | `100px` | Floating header height |
| `header-floating_navigation-bg-color` | alpha_color | `rgba(255,255,255,0.9)` | Floating header background color |
| `header-floating_navigation-bg-image` | background_img | — | Floating header background image |
| `header-floating_navigation-bg-is_fullscreen` | checkbox | `0` | Fullscreen floating header background |
| `header-floating_navigation-decoration` | images | `disabled` | Decoration: `disabled`, `shadow`, `content-width-line`, `line` |
| `header-style-floating-choose_logo` | radio | `custom` | Floating header logo: `custom`, `main`, `none` |
| `header-style-floating-logo-padding` | spacing | `0px` all | Floating logo padding |
| `header-floating-mobile-first_switch-logo` | radio | `desktop` | Floating mobile 1st breakpoint: `desktop`, `mobile` |
| `header-floating-mobile-second_switch-logo` | radio | `desktop` | Floating mobile 2nd breakpoint: `desktop`, `mobile` |
| `header-style-floating-mobile-logo-padding` | spacing | `0px` all | Floating mobile logo padding |

---

## Top Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `top-bar-height` | number | `0px` | Top bar height (0 disables the bar) |
| `top_bar-padding` | spacing | `0px 50px 0px 50px` | Top bar padding |
| `top_bar-switch_paddings` | number | `600px` | Top bar mobile padding breakpoint |
| `top_bar_mobile_paddings` | spacing | `0px 20px 0px 20px` | Top bar mobile padding |
| `top_bar-bg-color` | alpha_color | `#ffffff` | Top bar background color |
| `top_bar-bg-image` | background_img | — | Top bar background image |
| `top_bar-bg-style` | images | `content_line` | Top bar decoration: `disabled`, `content_line`, `full_width` |
| `top-bar-transparent_bg_color` | alpha_color | `rgba(0,0,0,0.5)` | Transparent top bar background color |

---

## Header Micro-widgets

The7 supports 7 micro-widget types that can be placed in various header positions. Enable per layout with `header-{layout}-show_elements` and configure placement with `header-{layout}-elements`.

### Micro-widget Placement (per layout)

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-classic-show_elements` | images | `0` | Enable micro-widgets for classic header |
| `header-classic-elements` | sortable | — | Micro-widgets layout for classic header |
| `header-classic-elements-near_menu_right-padding` | spacing | `0px 0px 0px 0px` | Navigation area padding |
| `header-classic-elements-near_logo_left-padding` | spacing | `0px 0px 0px 0px` | Left logo area padding |
| `header-classic-elements-near_logo_right-padding` | spacing | `0px 0px 0px 0px` | Right logo area padding |
| `header-inline-show_elements` | images | `0` | Enable for inline header |
| `header-inline-elements` | sortable | — | Micro-widgets layout for inline header |
| `header-split-show_elements` | images | `0` | Enable for split header |
| `header-split-elements` | sortable | — | Micro-widgets layout for split header |
| `header-side-show_elements` | images | `0` | Enable for side header |
| `header-side-elements` | sortable | — | Micro-widgets layout for side header |
| `header-top_line-show_elements` | images | `0` | Enable for top-line header |
| `header-top_line-elements` | sortable | — | Micro-widgets layout for top-line header |
| `header-side_line-show_elements` | images | `0` | Enable for side-line header |
| `header-side_line-elements` | sortable | — | Micro-widgets layout for side-line header |
| `header-menu_icon-show_elements` | images | `0` | Enable for menu icon header |
| `header-menu_icon-elements` | sortable | — | Micro-widgets layout for menu icon header |

### Social Icons Widget

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-elements-soc_icons-bg-size` | number | `26px` | Icons background size |
| `header-elements-soc_icons-size` | number | `16px` | Icons size |
| `header-elements-soc_icons_border_width` | number | `1px` | Border width |
| `header-elements-soc_icons_border_radius` | number | `100px` | Border radius |
| `header-elements-soc_icons_gap` | text | `4px` | Gap between icons |
| `header-elements-soc_icons-color` | alpha_color | `#fff` | Icons color (empty=accent) |
| `header-elements-soc_icons-bg` | radio | `accent` | Background mode: `disabled`, `accent`, `color`, `gradient` |
| `header-elements-soc_icons-bg-color` | alpha_color | `#ffffff` | Custom bg color (when mode=`color`) |
| `header-elements-soc_icons-bg-gradient` | gradient | — | Custom bg gradient (when mode=`gradient`) |

### Menu Widgets (2 instances)

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-elements-menu-style` | radio | `dropdown` | Desktop style: `dropdown`, `list` |
| `header-elements-menu-style-first-switch` | radio | `dropdown` | 1st breakpoint style: `dropdown`, `list` |
| `header-elements-menu-style-second-switch` | radio | `dropdown` | 2nd breakpoint style: `dropdown`, `list` |
| `header-elements-menu-icon` | select | `custom` | Dropdown icon: `disabled`, `custom` |
| `header-elements-menu_custom-icon` | icons_picker | `the7-mw-icon-dropdown-menu-bold` | Custom dropdown icon |
| `header-elements-menu2-*` | various | — | Menu 2 widget (same sub-options as Menu 1) |

### Login Widget

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-elements-login-caption` | text | `Login` | Login button text |
| `header-elements-logout-caption` | text | `Logout` | Logout button text |
| `header-elements-login-icon` | select | `custom` | Graphic icon: `disabled`, `custom` |
| `header-elements-login-custom-icon` | icons_picker | `the7-mw-icon-login` | Custom login icon |
| `header-elements-login-use_logout_url` | checkbox | — | Use custom logout link |
| `header-elements-login-url` | text | — | Custom login link URL |
| `header-elements-login-logout_url` | text | — | Custom logout link URL |

### Text Widgets (5 instances)

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-elements-text` | textarea | — | Text 1 content (HTML allowed) |
| `header-elements-text-2` | textarea | — | Text 2 content |
| `header-elements-text-3` | textarea | — | Text 3 content |
| `header-elements-text-4` | textarea | — | Text 4 content |
| `header-elements-text-5` | textarea | — | Text 5 content |

### Search Widget

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `microwidgets-search_style` | select | `popup` | Search style: `classic`, `animate_width`, `popup`, `overlay` |
| `header-elements-search-icon` | select | `custom` | Search icon: `disabled`, `custom` |
| `header-elements-search_custom-icon` | icons_picker | `the7-mw-icon-search` | Custom search icon |

### Multipurpose Widgets (Address, Email, Phone, Skype, Working Hours)

Each multipurpose widget (5 types) follows the pattern `header-elements-contact-{type}-*` where type is `address`, `email`, `phone`, `skype`, `clock`. Each has icon, layout, color, and padding sub-options.

### Button Widgets (2 instances)

Two button micro-widgets are available: `header-elements-button-1-*` and `header-elements-button-2-*`. Each has text, URL, target, icon, color, background, border, and padding sub-options.

---

## Stripes / Decorative Sections

The7 supports background stripes — page sections with independent background and content styling. Each stripe follows the pattern `stripes-stripe_{suffix}_*`:

| Option Pattern | Type | Default | Description |
|---------------|------|---------|-------------|
| `stripes-stripe_{suffix}_color` | color | varies | Stripe background color |
| `stripes-stripe_{suffix}_bg_image` | background_img | — | Stripe background image |
| `stripes-stripe_{suffix}_outline` | images | `hide` | Show/hide outlines: `show`, `hide` |
| `stripes-stripe_{suffix}_outline_color` | color | `#FFFFFF` | Outline color |
| `stripes-stripe_{suffix}_outline_opacity` | slider | `100` | Outline opacity (0-100%) |
| `stripes-stripe_{suffix}_content_boxes_bg_color` | color | `#FFFFFF` | Content boxes background |
| `stripes-stripe_{suffix}_content_boxes_bg_opacity` | slider | `100` | Content boxes opacity (0-100%) |
| `stripes-stripe_{suffix}_content_boxes_decoration` | images | `none` | Decoration: `none`, `shadow`, `outline` |
| `stripes-stripe_{suffix}_content_boxes_decoration_outline_color` | color | `#FFFFFF` | Decoration outline color |
| `stripes-stripe_{suffix}_content_boxes_decoration_outline_opacity` | slider | `100` | Decoration outline opacity |
| `stripes-stripe_{suffix}_headers_color` | color | varies | Stripe heading color |
| `stripes-stripe_{suffix}_text_color` | color | varies | Stripe text color |

---

## Social / Like Buttons

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `social_buttons-visibility` | images | `on_hover` | Share buttons appearance: `on_hover`, `allways` |
| `social_buttons-post-button_title` | text | — | Share button title for blog posts |
| `social_buttons-portfolio_post-button_title` | text | — | Share button title for portfolio |
| `social_buttons-photo-button_title` | text | — | Share button title for photos |
| `social_buttons-page-button_title` | text | — | Share button title for pages |
| `social_buttons-post` | social_buttons | array | Active social buttons for posts |
| `social_buttons-portfolio_post` | social_buttons | array | Active social buttons for portfolio |

Supported networks: Facebook, Twitter, LinkedIn, Pinterest, Email, WhatsApp, Telegram, Reddit, VK, Odnoklassniki, Viber, Pocket, Stumbleupon, Tumblr, Digg, MyWorld.

---

## Widget Areas

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `widgetareas` | fields_generator | array | Custom widget areas (dynamic add/remove) |

Each widget area entry has:
- `sidebar_name` (text) — Widget area display name
- `sidebar_desc` (textarea) — Widget area description (optional)

Default areas: Sidebar primary (ID: 1), Footer primary (ID: 2).

---

## Skins / Presets

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `preset` | skins | `none` | Pre-built design preset selection |

Available FSE skins (loaded dynamically): `fse-bakery`, `fse-business`, `fse-business-classic`, `fse-life-coach`, `fse-brewery`, `fse-corporate` (v4 only).

---

## FSE (Full Site Editing) Support

The7 has FSE variants with version-specific `theme.json` files (v1-v4):

| Version | Description |
|---------|-------------|
| v1 | Initial FSE support |
| v2 | Enhanced color palettes |
| v3 | Additional preset support |
| v4 | Latest with corporate preset |

Each `theme.json` includes:
- **Color palettes**: Neutral 50-950, Primary 50-950, Secondary colors
- **Gradients**: 14+ pre-defined gradients
- **Typography**: Font sizes, families, line heights
- **Custom templates**: Blank Page, Blank Page with Title
- **Layout**: Content/wide size, spacing patterns

> **Note**: FSE options are configured via theme.json and the Site Editor, not via `the7mk2` theme options. Use `mcm/get-global-styles` and `mcm/set-global-styles` for FSE variants.

---

## Footer Layout String Format

The `footer-layout` option uses a string format to define column widths:

| Value | Columns |
|-------|---------|
| `1/1` | 1 full-width column |
| `1/2+1/2` | 2 equal columns |
| `1/3+1/3+1/3` | 3 equal columns |
| `1/4+1/4+1/4+1/4` | 4 equal columns |
| `1/3+2/3` | 2 columns (narrow + wide) |
| `2/3+1/3` | 2 columns (wide + narrow) |
| `1/4+1/2+1/4` | 3 columns (narrow + wide + narrow) |

---

## Spacing Format

Spacing options use CSS-like strings: `"top right bottom left"`

```json
// Example: set footer padding
mcm/set-theme-options {"values": {"footer-padding": "60px 30px 60px 30px"}}
```
