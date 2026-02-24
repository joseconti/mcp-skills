# Avada — Complete Configurable Options Reference

Avada uses **three storage mechanisms** for configuration:

1. **Theme options** (`fusion_options` in `wp_options`): All visual styling options including logo URLs. Read via `mcm/get-theme-options` and update via `mcm/set-theme-options` (auto-detects `fusion_options` for Avada).
2. **Theme mods** (`theme_mods_Avada` in `wp_options`): `custom_logo` (attachment ID) and menu locations. Read via `mcm/get-theme-mod` and update via `mcm/set-theme-mod`.
3. **Page-level overrides** (post meta): Per-page settings with `pyre_` prefix. Read/write via `mcm/update-content`.

> **CRITICAL — Logo**: Avada stores logos as URLs in `fusion_options` (e.g., `"logo": {"url": "..."}`) AND as attachment ID in `custom_logo` theme mod. **Set BOTH** for maximum compatibility.

> **CRITICAL — Typography**: Typography fields are arrays, NOT simple strings. See the Typography section for the required format.

> **CRITICAL — Color Palette**: Avada 7.x+ uses AWB global color palette. Many defaults reference `var(--awb-colorN)`. Set the palette first, then individual colors.

---

## 1. Colors

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `color_palette` | color-palette | AWB defaults | Global color palette (8 core colors) |
| `primary_color` | color-alpha | `var(--awb-color5)` | Primary accent color used across the site |

### AWB Global Color Variables

| Variable | Purpose |
|----------|---------|
| `--awb-color1` | Light/White (backgrounds) |
| `--awb-color2` | Secondary light |
| `--awb-color3` | Light gray |
| `--awb-color4` | Medium/accent |
| `--awb-color5` | Primary accent |
| `--awb-color6` | Dark accent |
| `--awb-color7` | Dark background |
| `--awb-color8` | Dark text |

---

## 2. Typography

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `typography_sets` | typography-sets | AWB defaults | Global typography presets |
| `body_typography` | typography | Font vars | Body text font settings |
| `h1_typography` | typography | 64px | Heading 1 font settings (includes margin-top/margin-bottom: default 0.67em/0.67em) |
| `h2_typography` | typography | AWB var | Heading 2 font settings (includes margin-top/margin-bottom: default 0em/1.1em) |
| `h3_typography` | typography | 36px | Heading 3 font settings (includes margin-top/margin-bottom: default 1em/1em) |
| `h4_typography` | typography | 24px | Heading 4 font settings (includes margin-top/margin-bottom: default 1.33em/1.33em) |
| `h5_typography` | typography | 20px | Heading 5 font settings (includes margin-top/margin-bottom: default 1.67em/1.67em) |
| `h6_typography` | typography | 16px | Heading 6 font settings (includes margin-top/margin-bottom: default 2.33em/2.33em) |
| `post_title_typography` | typography | 48px | Post title font settings (no margin-top/margin-bottom) |
| `post_titles_extras_typography` | typography | 20px | Post subtitle/extras font (no margin-top/margin-bottom) |
| `link_color` | color-alpha | `var(--awb-color8)` | Link color |
| `link_hover_color` | color-alpha | `var(--awb-color5)` | Link hover color |
| `link_decoration` | switch | `0` | Enable link text decoration |
| `link_decoration_line` | select | `none` | Decoration line type. Choices: none, underline, overline, line-through |
| `link_decoration_style` | select | `solid` | Decoration line style. Choices: solid, double, dotted, dashed, wavy |
| `link_decoration_thickness` | dimension | `1px` | Decoration line thickness |
| `link_decoration_underline_offset` | dimension | `auto` | Decoration underline offset from text |
| `link_decoration_line_hover` | select | `none` | Decoration line type on hover |
| `link_decoration_style_hover` | select | `solid` | Decoration style on hover |
| `link_decoration_thickness_hover` | dimension | `1px` | Decoration thickness on hover |
| `link_decoration_underline_offset_hover` | dimension | `auto` | Underline offset on hover |
| `link_decoration_exclusion` | select (multi) | `[]` | Exclude elements from link decoration |
| `custom_fonts` | repeater | `[]` | Custom font uploads (name + woff2/woff/ttf/svg/eot files) |
| `adobe_fonts_id` | text | empty | Adobe Fonts project ID |

### Typography field structure

Typography fields MUST be arrays with ALL properties:
```json
{
    "font-family": "Arial, sans-serif",
    "font-size": "16px",
    "font-weight": "400",
    "line-height": "1.6",
    "letter-spacing": "0",
    "font-style": "normal",
    "text-transform": "none",
    "color": "#333333"
}
```

**H1-H6 heading typography** also supports `margin-top` and `margin-bottom` within the same array. Post Title options do NOT have margin fields.

### Heading Margin Defaults

| Heading | margin-top | margin-bottom |
|---------|-----------|--------------|
| H1 | `0.67em` | `0.67em` |
| H2 | `0em` | `1.1em` |
| H3 | `1em` | `1em` |
| H4 | `1.33em` | `1.33em` |
| H5 | `1.67em` | `1.67em` |
| H6 | `2.33em` | `2.33em` |

---

## 3. Header

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header_position` | radio-buttonset | `top` | Header position. Choices: top, left, right |
| `header_layout` | radio-image | `v3` | Header layout version. Choices: v1 (logo left, nav right), v2 (logo left, nav+search right), v3 (logo centered between nav), v4 (logo left, search+tagline right), v5 (logo centered above nav), v6 (logo left, nav below), v7 (top bar above with full-width menu) |
| `slider_position` | radio-buttonset | `below` | Slider above/below header. Choices: below, above |
| `header_left_content` | select | `social_links` | Left header area content. Choices: contact_info, social_links, navigation, leave_empty |
| `header_right_content` | select | `navigation` | Right header area content. Choices: contact_info, social_links, navigation, leave_empty |
| `header_v4_content` | select | `tagline_and_search` | V4 header content type |
| `header_bg_color` | color-alpha | `var(--awb-color1)` | Header background color |
| `header_bg_image` | media | empty | Header background image |
| `header_bg_full` | switch | `0` | Full-width header bg image |
| `header_bg_parallax` | switch | `1` | Parallax header bg |
| `header_border_color` | color-alpha | transparent | Header border color |
| `header_shadow` | switch | `0` | Header shadow |
| `header_100_width` | switch | `0` | 100% width header |
| `header_padding` | spacing | `0px` all | Header padding (top/right/bottom/left) |
| `side_header_width` | slider | `280` | Side header width (px, min 0, max 800) |
| `header_number` | text | empty | Contact phone number in header |
| `header_email` | text | empty | Contact email in header |
| `header_tagline` | textarea | empty | Header tagline text |
| `header_banner_code` | code | empty | Header banner HTML code |

### Header Conditional Notes

**V4 Layout + Side Header Only:**
- `header_v4_content` only shows when `header_position != 'top'` AND `header_layout == 'v4'`
- `header_tagline` requires `header_layout == 'v4'` AND `header_v4_content` contains `'tagline'` AND `header_position != 'top'`
- `header_banner_code` requires `header_layout == 'v4'` AND `header_v4_content == 'banner'` AND `header_position != 'top'`

**Side Header Only** (`header_position` = left or right):
- `header_left_content` / `header_right_content` — only available with side headers (v2-v5 layouts)

**Top Header Only** (`header_position` = top):
- `slider_position` — slider above/below header (only for top position)
- `header_bg_parallax` — parallax bg effect (only for top position)

### Sticky Header

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header_sticky` | switch | `1` | Enable sticky header |
| `header_sticky_tablet` | switch | `0` | Enable sticky header on tablet |
| `header_sticky_mobile` | switch | `0` | Enable sticky header on mobile |
| `header_sticky_shrinkage` | switch | `0` | Shrink header on scroll |
| `header_sticky_shadow` | switch | `1` | Show shadow on sticky header |
| `header_sticky_bg_color` | color-alpha | `var(--awb-color1)` | Sticky header background color |
| `header_sticky_menu_color` | color-alpha | `var(--awb-color8)` | Sticky header menu text color |
| `header_sticky_nav_padding` | slider | `35` | Sticky header nav padding (px) |
| `header_sticky_nav_font_size` | dimension | `14px` | Sticky header nav font size |
| `header_sticky_type2_layout` | radio-buttonset | `menu_only` | Sticky header layout for type 2. Choices: menu_only, menu_and_logo |

### Top Header Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header_top_bg_color` | color-alpha | `var(--awb-color4)` | Top bar background color |
| `archive_header_bg_color` | color-alpha | `var(--awb-color1)` | Archive header background color |
| `tagline_font_size` | dimension | `16px` | Tagline font size |
| `tagline_font_color` | color-alpha | `var(--awb-color8)` | Tagline text color |

---

## 4. Page Title Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `page_title_bar` | radio-buttonset | `bar_and_content` | Display mode. Choices: bar_and_content (bar + content), content_only (content only), hide (disabled) |
| `page_title_bar_bs` | radio-buttonset | `none` | Below title bar. Choices: none, breadcrumbs, search_box |
| `page_title_bar_text` | radio-buttonset | `1` | Show page title text. Choices: 1 (yes), 0 (no) |
| `page_title_100_width` | switch | `0` | 100% width page title bar |
| `page_title_height` | dimension | `auto` | Page title bar height (px or auto) |
| `page_title_mobile_height` | dimension | `auto` | Mobile page title bar height |
| `page_title_bg_color` | color-alpha | `var(--awb-color2)` | Page title bar background color |
| `page_title_border_color` | color-alpha | `var(--awb-color3)` | Page title bar border color |
| `page_title_font_size` | dimension | `36px` | Page title font size |
| `page_title_line_height` | dimension | `auto` | Page title line height |
| `page_title_color` | color-alpha | `var(--awb-color8)` | Page title text color |
| `page_title_subheader_font_size` | dimension | `16px` | Subheading font size |
| `page_title_subheader_color` | color-alpha | `var(--awb-color8)` | Subheading text color |
| `page_title_alignment` | radio-buttonset | `left` | Title alignment. Choices: left, center, right |
| `page_title_bg` | media | empty | Page title bar background image |
| `page_title_bg_retina` | media | empty | Retina background image |
| `page_title_bg_full` | switch | `0` | 100% background image |
| `page_title_bg_parallax` | switch | `1` | Parallax background effect |
| `page_title_fading` | switch | `0` | Fading scrolling effect |

---

## 5. Breadcrumbs

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `breadcrumb_mobile` | switch | `0` | Show breadcrumbs on mobile devices |
| `breacrumb_prefix` | text | empty | Text before the breadcrumb menu (note: intentional typo in option ID) |
| `breacrumb_home_label` | text | empty | Home anchor text (leave empty for default "Home") |
| `breadcrumb_separator` | text | `/` | Separator character between breadcrumbs |
| `breadcrumbs_font_size` | dimension | `14px` | Breadcrumbs font size |
| `breadcrumbs_text_color` | color-alpha | `var(--awb-color8)` | Breadcrumbs text color |
| `breadcrumbs_text_hover_color` | color-alpha | `var(--awb-color4)` | Breadcrumbs text hover color |
| `breadcrumbs_prefix_color` | color-alpha | empty | Prefix text color (uses text color if empty) |
| `breadcrumbs_current_page_color` | color-alpha | empty | Current page color (uses text color if empty) |
| `breadcrumbs_separator_color` | color-alpha | empty | Separator color (uses text color if empty) |
| `breadcrumb_show_categories` | switch | `1` | Show post categories/terms in breadcrumb path |
| `breadcrumb_show_post_type_archive` | switch | `0` | Show post type archives in breadcrumb path |
| `breadcrumb_show_leaf` | switch | `1` | Show post name in breadcrumb path |

---

## 6. Menu / Navigation

### Main Menu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `nav_height` | slider | `94` | Navigation height in px (min 0, max 300) |
| `nav_typography` | typography | font vars | Main menu typography (array format) |
| `menu_highlight_style` | radio-buttonset | `bar` | Menu highlight style. Choices: bar, arrow, background |
| `menu_highlight_background` | color-alpha | `var(--awb-color4)` | Highlight background color |
| `nav_highlight_border` | slider | `3` | Highlight border size (px) |
| `nav_highlight_style` | color-alpha | `var(--awb-color4)` | Highlight bar/arrow color |
| `main_nav_highlight_radius` | dimension | `0` | Highlight border radius |
| `nav_padding` | slider | `48` | Nav item horizontal padding (px) |
| `menu_hover_first_color` | color-alpha | `var(--awb-color8)` | Menu first-level text color |
| `menu_h45_bg_color` | color-alpha | transparent | Header v4/v5 menu background |
| `menu_icon_position` | radio-buttonset | `left` | Menu icon position. Choices: left, right, top, bottom |
| `menu_icon_size` | slider | `16` | Menu icon size (px) |
| `menu_icon_color` | color-alpha | auto | Menu icon color |
| `menu_icon_hover_color` | color-alpha | auto | Menu icon hover color |
| `main_nav_icon_circle` | switch | `0` | Circular background for menu icons |
| `menu_text_align` | radio-buttonset | `left` | Menu text alignment. Choices: left, center, right |
| `main_nav_search_icon` | switch | `1` | Show search icon in navigation |
| `main_nav_search_layout` | radio-buttonset | `dropdown` | Search layout. Choices: dropdown, overlay |
| `menu_display_dropdown_indicator` | radio-buttonset | `parent` | Dropdown indicator arrows. Choices: parent, all, none |
| `menu_arrow_size` | dimensions | `23x12` | Dropdown arrow size (width x height) |
| `menu_thumbnail_size` | dimensions | auto | Menu item thumbnail size |

### Dropdown / Submenu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `nav_dropdown_font_size` | dimension | `14px` | Dropdown menu font size |
| `dropdown_menu_width` | slider | `200` | Dropdown menu width (px) |
| `dropdown_menu_top_border_size` | slider | `3` | Dropdown top border size (px) |
| `main_menu_sub_menu_animation` | radio-buttonset | `fade` | Submenu animation. Choices: fade, slide |
| `mainmenu_dropdown_vertical_padding` | slider | `12` | Dropdown item vertical padding (px) |
| `mainmenu_dropdown_display_divider` | switch | `1` | Show dividers between dropdown items |
| `menu_sub_bg_color` | color-alpha | `var(--awb-color1)` | Dropdown background color |
| `menu_bg_hover_color` | color-alpha | `var(--awb-color2)` | Dropdown hover background color |
| `menu_sub_color` | color-alpha | `var(--awb-color8)` | Dropdown text color |
| `menu_sub_sep_color` | color-alpha | `var(--awb-color3)` | Dropdown separator color |
| `submenu_slideout` | switch | `0` | Slideout submenu effect |

### Mega Menu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `megamenu_shadow` | switch | `1` | Mega menu shadow |
| `megamenu_width` | radio-buttonset | `site_width` | Mega menu width. Choices: site_width, full_width, custom_width |
| `megamenu_base_width` | slider | `1200` | Custom mega menu width (px) |
| `megamenu_interior_content_width` | radio-buttonset | `col_total` | Interior content width. Choices: col_total, full_width |
| `megamenu_title_size` | dimension | `14px` | Mega menu column title size |
| `megamenu_item_vertical_padding` | slider | `7` | Item vertical padding (px) |
| `megamenu_item_display_divider` | switch | `1` | Show dividers between mega menu items |

### Flyout Menu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `flyout_menu_direction` | select | `fade` | Flyout animation direction. Choices: fade, left, right, bottom, top |
| `flyout_menu_background_color` | color-alpha | `var(--awb-color1)` | Flyout menu background |
| `flyout_menu_icon_color` | color-alpha | `var(--awb-color8)` | Flyout toggle icon color |
| `flyout_menu_icon_hover_color` | color-alpha | `var(--awb-color4)` | Flyout toggle icon hover color |
| `flyout_menu_icon_font_size` | dimension | `20px` | Flyout icon font size |
| `flyout_menu_item_padding` | slider | `15` | Flyout menu item padding (px) |
| `flyout_nav_icons_padding` | slider | `25` | Flyout nav icons padding (px) |

### Top Secondary Menu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `snav_font_size` | dimension | `12px` | Secondary nav font size |
| `snav_color` | color-alpha | `var(--awb-color1)` | Secondary nav text color |
| `sec_menu_lh` | dimension | `44px` | Secondary menu line height |
| `topmenu_dropwdown_width` | slider | `180` | Top menu dropdown width (px) |
| `header_top_first_border_color` | color-alpha | `var(--awb-color3)` | Top bar first border color |
| `header_top_menu_bg_hover_color` | color-alpha | transparent | Top menu hover background |
| `header_top_menu_sub_color` | color-alpha | `var(--awb-color8)` | Top submenu text color |
| `header_top_menu_sub_hover_color` | color-alpha | `var(--awb-color4)` | Top submenu hover text color |
| `header_top_menu_sub_sep_color` | color-alpha | `var(--awb-color3)` | Top submenu separator color |
| `header_top_sub_bg_color` | color-alpha | `var(--awb-color1)` | Top submenu background |

### Mobile Menu

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `mobile_menu_design` | radio-buttonset | `modern` | Mobile menu design. Choices: modern, classic, flyout |
| `mobile_menu_typography` | typography | font vars | Mobile menu typography (array format) |
| `mobile_menu_text_align` | radio-buttonset | `left` | Mobile menu text alignment |
| `mobile_nav_padding` | slider | `25` | Mobile nav item padding (px) |
| `mobile_menu_nav_height` | slider | `44` | Mobile menu item height (px) |
| `mobile_menu_background_color` | color-alpha | `var(--awb-color1)` | Mobile menu background |
| `mobile_menu_hover_color` | color-alpha | `var(--awb-color2)` | Mobile menu hover background |
| `mobile_menu_font_hover_color` | color-alpha | `var(--awb-color4)` | Mobile menu hover text color |
| `mobile_menu_border_color` | color-alpha | `var(--awb-color3)` | Mobile menu border color |
| `mobile_menu_toggle_color` | color-alpha | `var(--awb-color8)` | Mobile hamburger icon color |
| `mobile_menu_icons_top_margin` | slider | `0` | Mobile menu icons top margin (px) |
| `mobile_menu_submenu_indicator` | switch | `1` | Show submenu expand indicators |
| `mobile_nav_submenu_slideout` | switch | `0` | Slideout submenu on mobile |
| `mobile_header_bg_color` | color-alpha | `var(--awb-color1)` | Mobile header background |
| `mobile_archive_header_bg_color` | color-alpha | `var(--awb-color1)` | Mobile archive header background |

---

## 7. Footer

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `footer_widgets` | switch | `1` | Show footer widgets area |
| `footer_widgets_columns` | slider | `4` | Number of widget columns (1-6) |
| `footer_widgets_center_content` | switch | `0` | Center widget content |
| `footer_copyright` | switch | `1` | Show copyright bar |
| `footer_copyright_center_content` | switch | `0` | Center copyright content |
| `footer_text` | code | Template | Copyright HTML (supports shortcodes) |
| `footer_100_width` | switch | `0` | Full-width footer |
| `footer_special_effects` | radio | `none` | Footer special effects. Choices: none, footer_parallax_effect, footer_area_bg_parallax, footer_sticky, footer_sticky_with_parallax_bg_image |
| `footer_bg_color` | color-alpha | `var(--awb-color7)` | Footer background color |
| `footer_border_size` | slider | `0` | Footer top border size (px) |
| `footer_border_color` | color-alpha | `var(--awb-color3)` | Footer top border color |
| `footer_divider_line` | switch | `0` | Show divider between columns |
| `footer_divider_line_size` | slider | `1` | Divider thickness (px) |
| `footer_divider_line_style` | select | `solid` | Divider style. Choices: solid, dashed, dotted, double |
| `footer_divider_color` | color-alpha | `var(--awb-color6)` | Divider color |
| `footer_area_padding` | spacing | `60px 0 64px 0` | Footer area padding |
| `footer_widgets_padding` | dimension | `16px` | Widget spacing |
| `footer_headings_typography` | typography | weight 600 | Footer heading font (array format) |
| `footer_text_color` | color-alpha | color1 opacity | Footer text color |
| `footer_link_color` | color-alpha | color1 reduced | Footer link color |
| `footer_link_color_hover` | color-alpha | `var(--awb-color4)` | Footer link hover color |

### Footer Background

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `footerw_bg_image` | media | empty | Footer background image |
| `footerw_bg_full` | switch | `0` | Full-width footer background |
| `footerw_bg_repeat` | select | `no-repeat` | Background repeat. Choices: repeat, repeat-x, repeat-y, no-repeat |
| `footerw_bg_pos` | select | `center center` | Background position |

### Copyright Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `copyright_padding` | spacing | `20px 0` | Copyright bar padding |
| `copyright_bg_color` | color-alpha | `var(--awb-color8)` | Copyright background color |
| `copyright_border_size` | slider | `0` | Copyright top border (px) |
| `copyright_border_color` | color-alpha | `var(--awb-color8)` | Copyright border color |
| `copyright_text_color` | color-alpha | reduced opacity | Copyright text color |
| `copyright_link_color` | color-alpha | reduced opacity | Copyright link color |
| `copyright_link_color_hover` | color-alpha | `var(--awb-color4)` | Copyright link hover color |
| `copyright_font_size` | dimension | `13px` | Copyright font size |

---

## 8. Sliding Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `slidingbar_widgets` | switch | `0` | Enable sliding bar |
| `mobile_slidingbar_widgets` | switch | `0` | Show sliding bar on mobile |
| `slidingbar_open_on_load` | switch | `0` | Open sliding bar on page load |
| `slidingbar_position` | radio-buttonset | `top` | Sliding bar position. Choices: top, right, bottom, left |
| `slidingbar_width` | dimension | `350px` | Sliding bar width (for left/right position) |
| `slidingbar_sticky` | switch | `0` | Sticky sliding bar toggle |
| `slidingbar_widgets_columns` | slider | `2` | Number of widget columns (1-6) |
| `slidingbar_column_alignment` | radio-buttonset | `top` | Column vertical alignment. Choices: top, center, bottom |
| `slidingbar_content_padding` | spacing | 30px all | Content padding |
| `slidingbar_content_align` | radio-buttonset | `left` | Content text alignment. Choices: left, center, right |
| `slidingbar_toggle_style` | radio-buttonset | `triangle` | Toggle button style. Choices: triangle, rectangle, circle, menu |
| `slidingbar_bg_color` | color-alpha | `var(--awb-color7)` | Background color |
| `slidingbar_divider_color` | color-alpha | AWB color6 | Divider line color |
| `slidingbar_toggle_icon_color` | color-alpha | `var(--awb-color1)` | Toggle icon color |
| `slidingbar_font_size` | dimension | `13px` | Widget title font size |
| `slidingbar_headings_color` | color-alpha | `var(--awb-color1)` | Widget heading color |
| `slidingbar_text_color` | color-alpha | reduced opacity | Text color |
| `slidingbar_link_color` | color-alpha | reduced opacity | Link color |
| `slidingbar_link_color_hover` | color-alpha | `var(--awb-color4)` | Link hover color |
| `slidingbar_border` | switch | `0` | Top border on toggle |

---

## 9. Sidebars

### Sidebar Styling

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `responsive_sidebar_order` | radio-buttonset | `after` | Mobile sidebar order. Choices: after (after content), before (before content) |
| `sidebar_sticky` | radio-buttonset | `none` | Sticky sidebar. Choices: none, single, dual |
| `sidebar_padding` | dimension | `0` | Sidebar content padding |
| `sidebar_bg_color` | color-alpha | transparent | Sidebar background color |
| `sidebar_widget_bg_color` | color-alpha | transparent | Widget title background color |
| `sidew_font_size` | dimension | `17px` | Widget heading font size |
| `sidebar_heading_color` | color-alpha | `var(--awb-color8)` | Widget heading color |

### Sidebar Assignments (per section)

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `default_sidebar_pos` | radio-buttonset | `right` | Default sidebar position for all content types. Choices: left, right |

Each section has 4 options: `*_sidebar`, `*_sidebar_2`, `*_global_sidebar`, `*_sidebar_position`.

**Pages:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `pages_sidebar` | select | `None` | Primary sidebar for pages |
| `pages_sidebar_2` | select | `None` | Secondary sidebar for pages |
| `pages_global_sidebar` | switch | `0` | Use same sidebars on all pages |
| `pages_sidebar_position` | radio-buttonset | `right` | Sidebar position. Choices: left, right |

**Blog Posts:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `posts_sidebar` | select | `None` | Primary sidebar for blog posts |
| `posts_sidebar_2` | select | `None` | Secondary sidebar |
| `posts_global_sidebar` | switch | `0` | Use same sidebars on all posts |
| `blog_sidebar_position` | radio-buttonset | `right` | Sidebar position |

**Blog Archive:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `blog_archive_sidebar` | select | `None` | Primary sidebar for blog archives |
| `blog_archive_sidebar_2` | select | `None` | Secondary sidebar |
| `blog_archive_sidebar_position` | radio-buttonset | `right` | Sidebar position |

**Portfolio:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `portfolio_sidebar` | select | `None` | Primary sidebar for portfolio posts |
| `portfolio_sidebar_2` | select | `None` | Secondary sidebar |
| `portfolio_global_sidebar` | switch | `0` | Use same sidebars on all portfolio |
| `portfolio_sidebar_position` | radio-buttonset | `right` | Sidebar position |

**Portfolio Archive:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `portfolio_archive_sidebar` | select | `None` | Primary sidebar |
| `portfolio_archive_sidebar_2` | select | `None` | Secondary sidebar |
| `portfolio_archive_sidebar_position` | radio-buttonset | `right` | Sidebar position |

**Search:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `search_sidebar` | select | `None` | Primary sidebar for search results |
| `search_sidebar_2` | select | `None` | Secondary sidebar |
| `search_sidebar_position` | radio-buttonset | `right` | Sidebar position |

**WooCommerce Products:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woo_sidebar` | select | `None` | Primary sidebar for products |
| `woo_sidebar_2` | select | `None` | Secondary sidebar |
| `woo_global_sidebar` | switch | `0` | Use same sidebars on all products |
| `woo_sidebar_position` | radio-buttonset | `right` | Sidebar position |

**WooCommerce Archive:**
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woocommerce_archive_sidebar` | select | `None` | Primary sidebar |
| `woocommerce_archive_sidebar_2` | select | `None` | Secondary sidebar |
| `woocommerce_archive_sidebar_position` | radio-buttonset | `right` | Sidebar position |

**Events Calendar** (requires The Events Calendar plugin):
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `ec_sidebar` | select | `None` | Primary sidebar for events |
| `ec_sidebar_2` | select | `None` | Secondary sidebar |
| `ec_global_sidebar` | switch | `0` | Use same sidebars for all events |
| `ec_sidebar_pos` | radio-buttonset | `right` | Sidebar position |

**bbPress** (requires bbPress plugin):
| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `ppbress_sidebar` | select | `None` | Primary sidebar for forums |
| `ppbress_sidebar_2` | select | `None` | Secondary sidebar |
| `bbpress_global_sidebar` | switch | `0` | Use same sidebars for all forums |
| `bbpress_sidebar_position` | radio-buttonset | `right` | Sidebar position |

---

## 10. Blog

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `blog_title` | text | `Blog` | Blog page title |
| `blog_subtitle` | text | empty | Blog subtitle |
| `blog_layout` | select | `large` | Blog layout. Choices: large, medium, large-alternate, medium-alternate, grid, timeline, masonry |
| `blog_archive_layout` | select | `large` | Archive layout (same choices) |
| `blog_pagination_type` | radio-buttonset | `pagination` | Pagination. Choices: pagination, infinite_scroll, load_more_button |
| `blog_archive_grid_columns` | slider | `3` | Grid columns (1-6) |
| `blog_archive_grid_column_spacing` | slider | `40` | Grid column spacing (px) |
| `blog_equal_heights` | switch | `0` | Equal height cards in grid |
| `blog_layout_alignment` | radio-buttonset | empty | Content alignment |
| `content_length` | radio-buttonset | `excerpt` | Content display. Choices: excerpt, full_content |
| `excerpt_length_blog` | slider | `10` | Excerpt word count |
| `strip_html_excerpt` | switch | `1` | Strip HTML from excerpts |
| `featured_images` | switch | `1` | Show featured images on archives |
| `featured_images_single` | switch | `1` | Show featured on single posts |
| `blog_width_100` | switch | `0` | 100% width blog posts |
| `blog_pn_nav` | switch | `1` | Previous/next navigation |
| `blog_post_title` | radio-buttonset | `below` | Post title position. Choices: below, above, inside_fimage |
| `blog_post_meta_position` | radio-buttonset | `below_article` | Meta position |
| `social_sharing_box` | switch | `1` | Show social sharing box |
| `author_info` | switch | `1` | Show author info |
| `related_posts` | switch | `1` | Show related posts |
| `blog_comments` | switch | `1` | Show comments |
| `post_meta` | switch | `1` | Show post meta |
| `post_meta_author` | switch | `1` | Show author in meta |
| `post_meta_date` | switch | `1` | Show date in meta |
| `post_meta_cats` | switch | `1` | Show categories in meta |
| `post_meta_comments` | switch | `1` | Show comment count |
| `post_meta_read` | switch | `1` | Show read more link |
| `post_meta_tags` | switch | `0` | Show tags in meta |
| `meta_font_size` | dimension | `13px` | Meta font size |
| `date_format` | text | empty | Custom PHP date format |
| `dates_box_color` | color-alpha | `var(--awb-color2)` | Date box background color |
| `blog_archive_grid_padding` | spacing | `0px` all | Grid card padding |
| `blog_show_page_title_bar` | select | `default` | Show page title bar on blog |
| `blog_page_title_bar` | select | `default` | Blog page title bar override |
| `alternate_date_format_day` | text | `j` | Alternate date format (day) |
| `alternate_date_format_month_year` | text | `M, Y` | Alternate date format (month/year) |
| `timeline_date_format` | text | `F j, Y` | Timeline layout date format |

### Blog Load More

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `blog_load_more_posts_button_bg_color` | color-alpha | `var(--awb-color7)` | Load more button background |
| `blog_load_more_posts_button_text_color` | color-alpha | `var(--awb-color1)` | Load more button text |
| `blog_load_more_posts_hover_button_bg_color` | color-alpha | `var(--awb-color5)` | Load more hover background |
| `blog_load_more_posts_hover_button_text_color` | color-alpha | `var(--awb-color1)` | Load more hover text |

---

## 11. Portfolio

### Portfolio Archive

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `portfolio_archive_layout` | select | `portfolio-one` | Archive layout. Choices: portfolio-one, portfolio-two, portfolio-three, portfolio-four, portfolio-five, portfolio-six |
| `portfolio_archive_featured_image_size` | radio-buttonset | `full` | Image size. Choices: full, fixed, auto |
| `portfolio_archive_columns` | slider | `3` | Number of columns (1-6) |
| `portfolio_archive_column_spacing` | slider | `20` | Column spacing (px) |
| `portfolio_equal_heights` | switch | `0` | Equal height cards |
| `portfolio_archive_one_column_text_position` | radio-buttonset | `below` | Text position (1-col layout). Choices: below, next |
| `portfolio_archive_items` | slider | `10` | Items per page |
| `portfolio_archive_text_layout` | radio-buttonset | `unboxed` | Text area style. Choices: unboxed, boxed |
| `portfolio_archive_content_length` | radio-buttonset | `excerpt` | Content type. Choices: excerpt, full_content, no_text |
| `portfolio_archive_excerpt_length` | slider | `10` | Excerpt word count |
| `portfolio_archive_strip_html_excerpt` | switch | `1` | Strip HTML from excerpts |
| `portfolio_archive_title_display` | radio-buttonset | `all` | Title display. Choices: all, title, cats, none |
| `portfolio_archive_text_alignment` | radio-buttonset | `left` | Text alignment. Choices: left, center, right |
| `portfolio_archive_layout_padding` | spacing | `25px` all | Card padding |
| `portfolio_archive_pagination_type` | radio-buttonset | `pagination` | Pagination. Choices: pagination, infinite_scroll, load_more_button |
| `portfolio_slug` | text | `portfolio-items` | Portfolio URL slug |
| `portfolio_with_front` | switch | `1` | Include front base in URL |
| `portfolio_meta_font_size` | dimension | `13px` | Meta font size |

### Portfolio Load More Colors

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `portfolio_load_more_posts_button_bg_color` | color-alpha | `var(--awb-color7)` | Load more background |
| `portfolio_load_more_posts_button_text_color` | color-alpha | `var(--awb-color1)` | Load more text |
| `portfolio_load_more_posts_hover_button_bg_color` | color-alpha | `var(--awb-color5)` | Load more hover bg |
| `portfolio_load_more_posts_hover_button_text_color` | color-alpha | `var(--awb-color1)` | Load more hover text |
| `portfolio_archive_load_more_posts_button_bg_color` | color-alpha | `var(--awb-color7)` | Archive load more background |
| `portfolio_archive_load_more_posts_button_text_color` | color-alpha | `var(--awb-color1)` | Archive load more text |
| `portfolio_archive_load_more_posts_hover_button_bg_color` | color-alpha | `var(--awb-color5)` | Archive load more hover bg |
| `portfolio_archive_load_more_posts_hover_button_text_color` | color-alpha | `var(--awb-color1)` | Archive load more hover text |

### Portfolio Single

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `portfolio_pn_nav` | switch | `1` | Previous/next navigation |
| `portfolio_width_100` | switch | `0` | 100% width for single |
| `portfolio_featured_image_width` | radio-buttonset | `half` | Featured image width. Choices: full, half, auto |
| `portfolio_featured_images` | switch | `1` | Show featured images |
| `show_first_featured_image` | switch | `1` | Show first featured image |
| `portfolio_project_desc_title` | switch | `1` | Show project description title |
| `portfolio_project_details` | switch | `1` | Show project details |
| `portfolio_link_icon_target` | switch | `0` | Open project URL in new window |
| `portfolio_author` | switch | `1` | Show author info |
| `portfolio_social_sharing_box` | switch | `1` | Show social sharing |
| `portfolio_related_posts` | switch | `1` | Show related projects |
| `portfolio_comments` | switch | `0` | Show comments |

---

## 12. Search

### Search Form

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `search_filter_results` | switch | `0` | Show content type filter in search results |
| `search_content` | select (multi) | all types | Content types to search |
| `search_limit_to_post_titles` | switch | `0` | Limit search to post titles only |
| `search_add_woo_product_skus` | switch | `0` | Include WooCommerce SKUs in search |
| `search_form_design` | select | `classic` | Form design style. Choices: classic, clean, live |
| `live_search` | switch | `0` | Enable live/AJAX search |
| `live_search_min_char_count` | slider | `4` | Minimum characters for live search |
| `live_search_results_per_page` | slider | `100` | Max live search results |
| `live_search_results_height` | slider | `250` | Results dropdown height (px) |
| `live_search_display_featured_image` | switch | `1` | Show images in live results |
| `live_search_display_post_type` | switch | `0` | Show post type labels |

### Search Results Page

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `search_layout` | select | `large` | Results layout. Choices: large, medium, large-alternate, medium-alternate, grid, timeline, masonry |
| `search_results_per_page` | slider | `10` | Results per page |
| `search_pagination_type` | radio-buttonset | `pagination` | Pagination. Choices: pagination, infinite_scroll, load_more_button |
| `search_grid_columns` | slider | `3` | Grid columns (1-6) |
| `search_grid_column_spacing` | slider | `40` | Grid column spacing (px) |
| `search_content_length` | radio-buttonset | `excerpt` | Content display. Choices: excerpt, full_content, no_text |
| `search_excerpt_length` | slider | `10` | Excerpt word count |
| `search_strip_html_excerpt` | switch | `1` | Strip HTML from excerpts |
| `search_featured_images` | switch | `1` | Show featured images |
| `search_meta` | switch | `1` | Show post meta |
| `search_new_search_position` | radio-buttonset | `above` | New search field position. Choices: above, below, hidden |

---

## 13. Social Media

### Social Media Icons

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `social_media_icons` | repeater | default set | Social media icons list. Each item: `icon` (network name), `url` (profile URL), `custom_title`, `custom_source` (custom icon media) |

### Header Social Icon Styling

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header_social_links_font_size` | dimension | `16px` | Icon font size |
| `header_social_links_tooltip_placement` | radio-buttonset | `bottom` | Tooltip position. Choices: top, right, bottom, left, none |
| `header_social_links_color_type` | radio-buttonset | `custom` | Color mode. Choices: brand, custom |
| `header_social_links_icon_color` | color-alpha | `var(--awb-color8)` | Icon color |
| `header_social_links_boxed` | switch | `0` | Boxed icons |
| `header_social_links_box_color` | color-alpha | transparent | Box background color |
| `header_social_links_boxed_radius` | dimension | `4px` | Box border radius |
| `header_social_links_boxed_padding` | dimension | `8px` | Box padding |

### Footer Social Icon Styling

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `icons_footer` | switch | `1` | Show social icons in footer |
| `footer_social_links_font_size` | dimension | `16px` | Icon font size |
| `footer_social_links_tooltip_placement` | radio-buttonset | `top` | Tooltip position |
| `footer_social_links_color_type` | radio-buttonset | `custom` | Color mode. Choices: brand, custom |
| `footer_social_links_icon_color` | color-alpha | reduced opacity | Icon color |
| `footer_social_links_boxed` | switch | `0` | Boxed icons |
| `footer_social_links_box_color` | color-alpha | transparent | Box background color |
| `footer_social_links_boxed_radius` | dimension | `4px` | Box border radius |
| `footer_social_links_boxed_padding` | dimension | `8px` | Box padding |

### Social Sharing Box

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `sharing_social_tagline` | text | `Share This Story...` | Sharing box tagline |
| `sharing_box_tagline_text_color` | color-alpha | `var(--awb-color8)` | Tagline text color |
| `social_bg_color` | color-alpha | `var(--awb-color2)` | Sharing box background |
| `social_sharing_padding` | spacing | 25px all | Sharing box padding |
| `social_sharing` | select (multi) | fb,tw,reddit... | Networks to display (facebook, twitter, reddit, linkedin, whatsapp, tumblr, pinterest, vk, xing, email) |
| `sharing_social_links_font_size` | dimension | `16px` | Icon font size |
| `sharing_social_links_tooltip_placement` | radio-buttonset | `top` | Tooltip position |
| `sharing_social_links_color_type` | radio-buttonset | `custom` | Color mode. Choices: brand, custom |
| `sharing_social_links_icon_color` | color-alpha | `var(--awb-color8)` | Icon color |
| `sharing_social_links_boxed` | switch | `0` | Boxed icons |
| `sharing_social_links_box_color` | color-alpha | transparent | Box background color |
| `sharing_social_links_boxed_radius` | dimension | `4px` | Box border radius |
| `sharing_social_links_boxed_padding` | dimension | `8px` | Box padding |

---

## 14. WooCommerce

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woo_items` | slider | `12` | Products per page |
| `woocommerce_shop_page_columns` | slider | `4` | Shop page columns |
| `woocommerce_related_columns` | slider | `4` | Related products columns |
| `woocommerce_archive_page_columns` | slider | `3` | Archive page columns |
| `woocommerce_archive_grid_column_spacing` | slider | `40` | Archive grid spacing (px) |
| `woocommerce_product_images_layout` | radio-buttonset | `avada` | Product image layout. Choices: avada, woocommerce |
| `woocommerce_product_images_zoom` | switch | `1` | Image zoom on hover |
| `woocommerce_single_gallery_size` | dimension | `500px` | Gallery size |
| `woocommerce_gallery_thumbnail_width` | slider | `200` | Thumbnail width (px) |
| `woocommerce_gallery_thumbnail_columns` | slider | `4` | Thumbnail columns |
| `woocommerce_product_images_thumbnail_position` | radio-buttonset | `bottom` | Thumbnail position. Choices: bottom, left, right |
| `woocommerce_enable_quick_view` | switch | `0` | Enable quick view |
| `woocommerce_variations` | switch | `1` | Show variations on shop |
| `woocommerce_avada_ordering` | switch | `1` | Custom Avada ordering/sorting |
| `woocommerce_disable_crossfade_effect` | switch | `1` | Disable image crossfade |
| `woocommerce_one_page_checkout` | switch | `0` | One-page checkout |
| `woocommerce_enable_order_notes` | switch | `1` | Order notes field |
| `woocommerce_acc_link_main_nav` | switch | `0` | Account link in main nav |
| `woocommerce_cart_link_main_nav` | switch | `1` | Cart link in main nav |
| `woocommerce_cart_counter` | switch | `0` | Cart counter badge |
| `woocommerce_cart_link_top_nav` | switch | `1` | Cart link in top nav |
| `woocommerce_acc_link_top_nav` | switch | `0` | Account link in top nav |
| `woocommerce_toggle_grid_list` | switch | `1` | Show grid/list toggle on shop |
| `woocommerce_equal_heights` | switch | `0` | Equal height product boxes |
| `woocommerce_product_view` | switch | `1` | Product view (image rollover) |
| `woocommerce_product_box_design` | spacing | `0px` all | Product box padding |
| `woocommerce_product_tab_design` | radio-buttonset | `horizontal` | Product tabs design. Choices: horizontal, vertical |
| `woocommerce_social_links` | switch | `1` | Show social links on product |
| `woocommerce_single_ajax_cart` | switch | `0` | AJAX add to cart on single product |
| `product_width_100` | switch | `0` | 100% width single product |
| `woocommerce_disable_crossfade_effect` | switch | `1` | Disable image crossfade on shop |

### WooCommerce Sale Badge

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woo_sale_badge_shape` | radio-buttonset | `rectangle` | Sale badge shape. Choices: rectangle, circle |
| `woo_sale_badge_text` | text | `Sale!` | Sale badge text |
| `woo_sale_badge_bg_color` | color-alpha | `var(--awb-color4)` | Sale badge background |
| `woo_sale_badge_text_color` | color-alpha | `var(--awb-color1)` | Sale badge text color |
| `woo_sale_badge_text_size` | dimension | `12px` | Sale badge font size |
| `woo_sale_badge_border_color` | color-alpha | transparent | Sale badge border color |
| `woo_sale_badge_border_radius` | spacing | `0px` | Sale badge border radius |
| `woo_sale_badge_padding` | spacing | `5px 8px` | Sale badge padding |

### WooCommerce Out of Stock Badge

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woo_outofstock_badge_shape` | radio-buttonset | `rectangle` | Out of stock badge shape |
| `woo_outofstock_badge_text` | text | `Out of stock` | Badge text |
| `woo_outofstock_badge_bg_color` | color-alpha | `var(--awb-color7)` | Badge background |
| `woo_outofstock_badge_text_color` | color-alpha | `var(--awb-color1)` | Badge text color |
| `woo_outofstock_badge_text_size` | dimension | `12px` | Badge font size |
| `woo_outofstock_badge_border_color` | color-alpha | transparent | Badge border color |
| `woo_outofstock_badge_border_radius` | spacing | `0px` | Badge border radius |
| `woo_outofstock_badge_padding` | spacing | `5px 8px` | Badge padding |

### WooCommerce Quantity Selector

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `qty_size` | dimensions | auto | Quantity input dimensions |
| `qty_font_size` | dimension | `12px` | Quantity font size |
| `qty_bg_color` | color-alpha | transparent | Quantity background |
| `qty_bg_hover_color` | color-alpha | `var(--awb-color2)` | Quantity hover background |

### WooCommerce Cart / Dropdowns

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woo_icon_font_size` | dimension | `18px` | Cart/account icon size |
| `woo_cart_bg_color` | color-alpha | transparent | Cart dropdown background |
| `woo_dropdown_bg_color` | color-alpha | `var(--awb-color1)` | Cart dropdown menu bg |
| `woo_dropdown_text_color` | color-alpha | `var(--awb-color8)` | Cart dropdown text color |
| `woo_dropdown_border_color` | color-alpha | `var(--awb-color3)` | Cart dropdown border |

### WooCommerce Account Messages

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woo_acc_msg_1` | textarea | empty | My Account page custom message 1 |
| `woo_acc_msg_2` | textarea | empty | My Account page custom message 2 |

---

## 15. Events Calendar

Requires The Events Calendar plugin.

### General

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `ec_display_page_title` | radio-buttonset | `below` | Events page title position. Choices: above, below, disable |
| `primary_overlay_text_color` | color-alpha | `var(--awb-color1)` | Text color on primary color background |
| `ec_bar_bg_color` | color-alpha | `var(--awb-color2)` | Filter bar background color |
| `ec_bar_text_color` | color-alpha | `var(--awb-color8)` | Filter bar text color |
| `ec_calendar_heading_bg_color` | color-alpha | `var(--awb-color3)` | Monthly calendar heading background |
| `ec_calendar_bg_color` | color-alpha | `var(--awb-color3)` | Monthly calendar day background |
| `ec_tooltip_bg_color` | color-alpha | `var(--awb-color1)` | Popover/dropdown background |
| `ec_tooltip_bg_hover_color` | color-alpha | `var(--awb-color2)` | Popover/dropdown hover background |
| `ec_tooltip_body_color` | color-alpha | `var(--awb-color8)` | Popover/dropdown text color |
| `ec_border_color` | color-alpha | `var(--awb-color3)` | Calendar border color |
| `ec_hover_type` | select | `none` | Featured image hover. Choices: none, zoomin, zoomout, liftup |
| `ec_bg_list_view` | radio-buttonset | `cover` | List view image size. Choices: cover, auto |
| `ec_sep_heading_font_size` | dimension | `18px` | Separator heading font size |

### Events Single Posts

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `ec_all_events_link` | switch | `0` | Show "all events" link |
| `tec_display_featured_image_title` | switch | `1` | Show featured image and title |
| `events_social_sharing_box` | switch | `1` | Show social sharing box |
| `ec_meta_layout` | radio-buttonset | `sidebar` | Meta layout. Choices: sidebar, below_content, disabled |
| `ec_sidebar_width` | dimension | `32%` | Sidebar width |
| `ec_sidebar_2_1_width` | dimension | `21%` | Dual sidebar width 1 |
| `ec_sidebar_2_2_width` | dimension | `21%` | Dual sidebar width 2 |
| `ec_sidebar_bg_color` | color-alpha | `var(--awb-color2)` | Sidebar background |
| `ec_sidebar_padding` | dimension | `4%` | Sidebar padding |
| `ec_sidew_font_size` | dimension | `17px` | Widget heading font size |
| `ec_sidebar_widget_bg_color` | color-alpha | `var(--awb-color4)` | Widget title background |
| `ec_sidebar_heading_color` | color-alpha | `var(--awb-color8)` | Heading color |
| `ec_text_font_size` | slider | `14` | Text font size (px) |
| `ec_sidebar_text_color` | color-alpha | `var(--awb-color8)` | Text color |
| `ec_sidebar_link_color` | color-alpha | `var(--awb-color5)` | Link color |
| `ec_sidebar_divider_color` | color-alpha | `var(--awb-color3)` | Divider color |

---

## 16. bbPress

Requires bbPress plugin.

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `bbp_forum_base_font_size` | dimension | `12px` | Forum base font size |
| `bbp_forum_header_bg` | color-alpha | `#ebeaea` | Forum header background color |
| `bbp_forum_header_font_color` | color-alpha | `#747474` | Forum header font color |
| `bbp_forum_border_color` | color-alpha | `#ebeaea` | Forum border color |

---

## 17. Layout

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `layout` | radio-buttonset | `wide` | Site layout. Choices: wide, boxed |
| `site_width` | dimension | `1200px` | Maximum site width |
| `margin_offset` | spacing | `0px 0` | Site margin offset (top/bottom) |
| `scroll_offset` | radio-buttonset | `full` | Scroll offset behavior |
| `boxed_modal_shadow` | select | `none` | Boxed layout shadow. Choices: none, light, medium, hard |
| `main_padding` | spacing | `60px 0` | Main content area padding |
| `page_template` | radio-buttonset | `100_width` | Default page template |
| `hundredp_padding` | dimension | `30px` | 100% width template side padding |

---

## 18. Background

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `bg_color` | color-alpha | `var(--awb-color3)` | Body background color |
| `bg_image` | media | empty | Body background image |
| `bg_full` | switch | `0` | Full-screen body background |
| `bg_repeat` | select | `no-repeat` | Background repeat. Choices: repeat, repeat-x, repeat-y, no-repeat |
| `bg_pattern_option` | switch | `0` | Use pattern background |
| `bg_pattern` | radio-image | `pattern1` | Pattern selection (pattern1-pattern11) |
| `content_bg_color` | color-alpha | `var(--awb-color1)` | Content area background color |
| `content_bg_image` | media | empty | Content background image |
| `content_bg_full` | switch | `0` | Full content background |
| `content_bg_repeat` | select | `no-repeat` | Content background repeat |

---

## 19. Logo

Avada logos use `{"url": "..."}` format in fusion_options. You MUST also set `custom_logo` theme mod:

```
1. mcm/upload-media {"url": "https://example.com/logo.png", "title": "Site Logo"}
   → Returns: {"attachment_id": 42, "url": "https://yoursite.com/wp-content/uploads/logo.png"}

2. mcm/set-theme-options {"values": {"logo": {"url": "https://yoursite.com/wp-content/uploads/logo.png"}}}

3. mcm/set-theme-mod {"key": "custom_logo", "value": 42}
```

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `logo` | media | Avada logo | Main site logo (`{"url": "..."}`) |
| `logo_retina` | media | Avada retina | Retina/HiDPI logo |
| `sticky_header_logo` | media | empty | Sticky header logo |
| `sticky_header_logo_retina` | media | empty | Sticky retina logo |
| `mobile_logo` | media | empty | Mobile logo |
| `mobile_logo_retina` | media | empty | Mobile retina logo |
| `logo_alignment` | radio-buttonset | `left` | Logo alignment. Choices: left, center, right |
| `logo_margin` | spacing | `34px 0` | Logo margin |
| `logo_background` | switch | `0` | Enable logo background |
| `logo_background_color` | color-alpha | `var(--awb-color4)` | Logo background color |
| `logo_custom_link` | text | empty | Custom logo link URL |
| `fav_icon` | media | empty | Favicon (`{"url": "..."}`) |
| `fav_icon_apple_touch` | media | empty | Apple touch icon |
| `fav_icon_android` | media | empty | Android icon |

---

## 20. Responsive

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `responsive` | radio-buttonset | `1` | Enable responsive design |
| `grid_main_break_point` | slider | `1000` | Main breakpoint (px, min 0, max 2000) |
| `side_header_break_point` | slider | `800` | Side header breakpoint (px) |
| `content_break_point` | slider | `800` | Content breakpoint (px) |
| `sidebar_break_point` | slider | `800` | Sidebar breakpoint (px) |
| `mobile_zoom` | switch | `1` | Allow mobile zoom/pinch |
| `visibility_small` | slider | `640` | Small screen max width (px) |
| `visibility_medium` | slider | `1024` | Medium screen max width (px) |
| `typography_sensitivity` | slider | `0` | Responsive typography sensitivity (0=off, higher=more responsive) |
| `typography_factor` | slider | `1.5` | Typography scale factor |

---

## 21. Slideshows

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `posts_slideshow_number` | slider | `5` | Number of featured image boxes for blog/portfolio posts (1-30) |
| `slideshow_autoplay` | switch | `1` | Autoplay slideshows |
| `slideshow_smooth_height` | switch | `0` | Smooth height for different image sizes |
| `slideshow_speed` | slider | `7000` | Slideshow speed in ms (100-20000) |
| `pagination_video_slide` | switch | `0` | Show pagination circles below video slides |
| `slider_nav_box_dimensions` | dimensions | `30x30px` | Navigation box width/height |
| `slider_arrow_size` | dimension | `14px` | Navigation arrow font size |

---

## 22. Elastic Slider

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `tfes_dimensions` | dimensions | `100% x 400px` | Elastic slider width/height |
| `tfes_animation` | radio-buttonset | `sides` | Animation type. Choices: sides, center |
| `tfes_autoplay` | switch | `1` | Autoplay slides |
| `tfes_interval` | slider | `3000` | Slideshow interval in ms (0-30000) |
| `tfes_speed` | slider | `800` | Sliding speed in ms (0-5000) |
| `tfes_width` | slider | `150` | Thumbnail width in px (0-500) |
| `es_title_font_size` | dimension | `42px` | Title font size |
| `es_caption_font_size` | dimension | `20px` | Caption font size |
| `es_title_color` | color-alpha | `var(--awb-color8)` | Title color |
| `es_caption_color` | color-alpha | `var(--awb-color8)` | Caption color |

---

## 23. Lightbox

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `status_lightbox` | switch | `1` | Enable lightbox |
| `status_lightbox_single` | switch | `1` | Enable on single posts |
| `lightbox_behavior` | radio-buttonset | `all` | Image links behavior. Choices: all (open lightbox for all links to images), iLightbox (only for items with iLightbox class) |
| `lightbox_skin` | select | `metro-white` | Lightbox skin. Choices: light, dark, mac, metro-black, metro-white, parade, smooth |
| `lightbox_path` | radio-buttonset | `vertical` | Thumbnails bar position. Choices: vertical, horizontal |
| `lightbox_animation_speed` | radio-buttonset | `normal` | Animation speed. Choices: fast, normal, slow |
| `lightbox_zoom` | switch | `1` | Enable zoom in/out buttons |
| `lightbox_arrows` | switch | `1` | Show navigation arrows |
| `lightbox_gallery` | switch | `1` | Show gallery icon (grouped images) |
| `lightbox_loop` | switch | `1` | Loop through gallery images |
| `lightbox_autoplay` | switch | `0` | Autoplay gallery slideshow |
| `lightbox_slideshow_speed` | slider | `5000` | Autoplay speed in ms (1000-20000) |
| `lightbox_opacity` | slider | `0.9` | Background opacity (0.1-1.0) |
| `lightbox_title` | switch | `1` | Show image title |
| `lightbox_desc` | switch | `1` | Show image caption/description |
| `lightbox_social` | switch | `1` | Show social sharing in lightbox |
| `lightbox_deeplinking` | switch | `1` | Enable deeplinking (shareable URLs) |
| `lightbox_post_images` | switch | `1` | Automatically add post images to lightbox gallery |
| `lightbox_video_dimensions` | dimensions | `1280x720` | Video width/height (px) |

---

## 24. Forms

### Form Styling

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `form_input_height` | dimension | `33px` | Form input height |
| `form_text_size` | dimension | `13px` | Form text size |
| `form_bg_color` | color-alpha | `var(--awb-color1)` | Input background color |
| `form_text_color` | color-alpha | `var(--awb-color8)` | Input text color |
| `form_border_width` | slider | `1` | Input border width (px, 0-20) |
| `form_border_color` | color-alpha | `var(--awb-color3)` | Input border color |
| `form_focus_border_color` | color-alpha | `var(--awb-color4)` | Input focus border color |
| `form_border_radius` | slider | `0` | Input border radius (px, 0-50) |
| `form_views` | switch | `1` | Count form views |
| `form_views_counting` | radio-buttonset | `all` | View counting mode. Choices: all (count all views), unique (unique per day) |

### Turnstile (Cloudflare)

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `turnstile_site_key` | text | empty | Cloudflare Turnstile site key |
| `turnstile_secret_key` | text | empty | Cloudflare Turnstile secret key |
| `turnstile_appearance` | select | `always` | Widget appearance. Choices: always, execute, interaction-only |
| `turnstile_theme` | select | `auto` | Widget theme. Choices: auto, light, dark |
| `turnstile_size` | select | `normal` | Widget size. Choices: normal, compact, flexible |
| `turnstile_language` | text | `auto` | Widget language |
| `turnstile_comment_form` | switch | `0` | Use on WordPress comment forms |

### reCAPTCHA (Google)

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `recaptcha_version` | radio-buttonset | `v2` | Version. Choices: v2, v3 |
| `recaptcha_public` | text | empty | Site key |
| `recaptcha_private` | text | empty | Secret key |
| `recaptcha_color_scheme` | radio-buttonset | `light` | Color scheme. Choices: light, dark |
| `recaptcha_score` | slider | `0.5` | v3 score threshold (0.0-1.0) |
| `recaptcha_badge_position` | select | `inline` | v3 badge position. Choices: inline, bottomright, bottomleft, hide |
| `recaptcha_login_form` | switch | `0` | Use on WordPress login form |
| `recaptcha_comment_form` | switch | `0` | Use on WordPress comment forms |

### Third-Party Integrations

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `hubspot_api` | text | empty | HubSpot API key |
| `hubspot_key` | text | empty | HubSpot portal ID |
| `mailchimp_api` | text | empty | Mailchimp API key |
| `mailchimp_key` | text | empty | Mailchimp list ID |

---

## 25. Extra / Miscellaneous

### General

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `featured_image_placeholder` | switch | `1` | Show placeholder for missing featured images |
| `excerpt_base` | radio-buttonset | `words` | Excerpt base unit. Choices: words, characters |
| `disable_excerpts` | switch | `0` | Disable excerpt generation |
| `excerpt_read_more_symbol` | text | `[...]` | Excerpt read more symbol |
| `link_read_more` | switch | `0` | Link read more symbol to post |
| `avatar_shape` | radio-buttonset | `square` | Avatar shape. Choices: square, round |
| `comments_pages` | switch | `0` | Show comments on pages |
| `featured_images_pages` | switch | `1` | Show featured images on pages |
| `nofollow_social_links` | switch | `0` | Add nofollow to social links |
| `social_icons_new` | switch | `0` | Open social links in new window/tab |
| `custom_scrollbar` | switch | `1` | Custom scrollbar |
| `scrollbar_background` | color-alpha | `var(--awb-color3)` | Scrollbar background color |
| `scrollbar_handle` | color-alpha | `var(--awb-color6)` | Scrollbar handle color |
| `faq_slug` | text | `faq-items` | FAQ URL slug |
| `faq_with_front` | switch | `1` | Include front base in FAQ URL |
| `cloning_posts` | switch | `1` | Enable post/page cloning |

### Related Posts/Projects

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `related_posts_layout` | select | `title_on_rollover` | Related posts layout. Choices: title_on_rollover, title_below_image |
| `number_related_posts` | slider | `4` | Number of related posts (0-12) |
| `related_posts_columns` | slider | `4` | Related posts columns (1-6) |
| `related_posts_column_spacing` | slider | `40` | Column spacing (px) |
| `related_posts_image_size` | radio-buttonset | `fixed` | Image size. Choices: fixed, auto, cropped |
| `related_posts_autoplay` | switch | `0` | Autoplay carousel |
| `related_posts_speed` | slider | `5000` | Carousel speed (ms) |
| `related_posts_navigation` | switch | `1` | Show carousel navigation |
| `related_posts_swipe` | switch | `0` | Enable swipe carousel |
| `related_posts_swipe_items` | slider | `0` | Swipe items to display (0=auto) |

### Image Rollover

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `image_rollover` | switch | `1` | Enable image rollover effect |
| `image_rollover_direction` | select | `left` | Rollover direction. Choices: left, right, bottom_top, top_bottom, fade, center_horiz, center_vert |
| `image_rollover_icon_size` | slider | `15` | Rollover icon size (px) |
| `image_rollover_icons` | radio-buttonset | `linkzoom` | Rollover icons. Choices: linkzoom (link + zoom), link (link only), zoom (zoom only), no (none) |
| `title_image_rollover` | switch | `1` | Show title on rollover |
| `cats_image_rollover` | switch | `1` | Show categories on rollover |
| `icon_circle_image_rollover` | switch | `1` | Circular icon background |
| `image_gradient_top_color` | color-alpha | opacity 65% | Gradient top color |
| `image_gradient_bottom_color` | color-alpha | opacity 99% | Gradient bottom color |
| `image_rollover_text_color` | color-alpha | `#FFFFFF` | Rollover text color |
| `image_rollover_icon_color` | color-alpha | `#FFFFFF` | Rollover icon color |

### Pagination

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `pagination_sizing` | radio-buttonset | `auto` | Pagination sizing. Choices: auto, fixed |
| `pagination_width_height` | dimensions | auto | Fixed pagination dimensions |
| `pagination_box_padding` | spacing | 0 all | Pagination box padding |
| `pagination_border_width` | slider | `0` | Border width (px) |
| `pagination_border_radius` | slider | `0` | Border radius (px) |
| `pagination_text_display` | switch | `1` | Show "Previous/Next" text |
| `pagination_font_size` | dimension | `14px` | Font size |
| `pagination_range` | slider | `1` | Number of page numbers to show |
| `pagination_start_end_range` | slider | `0` | Start/end range pages to show |

### Grid / Masonry

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `timeline_bg_color` | color-alpha | transparent | Timeline background color |
| `timeline_color` | color-alpha | `var(--awb-color3)` | Timeline line color |
| `grid_separator_style_type` | select | `none` | Grid separator style. Choices: none, single, double, shadow |
| `grid_separator_color` | color-alpha | `var(--awb-color3)` | Separator color |
| `masonry_grid_ratio` | slider | `1.5` | Masonry image aspect ratio |
| `masonry_width_double` | slider | `2000` | Double-width image threshold (px) |

### Scroll to Top

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `status_totop` | switch | `1` | Show scroll to top button |
| `totop_position` | radio-buttonset | `right` | Button position. Choices: left, right |
| `totop_border_radius` | slider | `6` | Border radius (px, 0-50) |
| `totop_background` | color-alpha | `var(--awb-color4)` | Button background color |
| `totop_background_hover` | color-alpha | `var(--awb-color5)` | Button hover background |
| `totop_icon_color` | color-alpha | `var(--awb-color1)` | Icon color |
| `totop_icon_hover` | color-alpha | `var(--awb-color1)` | Icon hover color |
| `totop_scroll_progress` | switch | `0` | Show scroll progress ring |
| `totop_scroll_down_only` | switch | `0` | Show only when scrolling down |

---

## 26. Contact Template

### Contact Form

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `email_address` | text | empty | Email address for contact page template form |
| `contact_comment_position` | radio-buttonset | `below` | Comment area position. Choices: above, below |
| `contact_form_privacy_checkbox` | switch | `0` | Show data privacy consent checkbox |
| `contact_form_privacy_label` | textarea | GDPR text | Privacy checkbox label (supports HTML) |

### Google Map

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `gmap_api` | text | empty | Google Maps API key (applies to builder element too) |
| `gmap_api_type` | radio-buttonset | `js` | API type. Choices: js (JavaScript API), embed (Embed API, free) |
| `gmap_embed_address` | text | empty | Embed API address |
| `gmap_embed_map_type` | radio-buttonset | `roadmap` | Embed map type. Choices: roadmap, satellite |
| `gmap_address` | textarea | default address | JS API address (use \| for multiple) |
| `gmap_type` | select | `roadmap` | JS API map type. Choices: roadmap, satellite, hybrid, terrain |
| `gmap_dimensions` | dimensions | `100% x 415px` | Map width/height |
| `gmap_topmargin` | dimension | `55px` | Map top margin (non-100% width) |
| `map_zoom_level` | slider | `8` | Zoom level (0-22) |
| `map_pin` | switch | `1` | Show address pin |
| `gmap_pin_animation` | switch | `1` | Pin animation on load |
| `map_popup` | switch | `0` | Popup on click |
| `map_scrollwheel` | switch | `1` | Zoom with scroll wheel |
| `map_scale` | switch | `1` | Show map scale |
| `map_zoomcontrol` | switch | `1` | Show zoom control icons |

### Google Map Styling

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `map_styling` | select | `default` | Map styling. Choices: default, theme, custom |
| `map_overlay_color` | color-alpha | `var(--awb-color4)` | Custom overlay color |
| `map_infobox_styling` | select | `default` | Info box style. Choices: default, custom |
| `map_infobox_content` | textarea | empty | Custom info box content (use \| for multiple) |
| `map_infobox_bg_color` | color-alpha | `var(--awb-color5)` | Info box background |
| `map_infobox_text_color` | color-alpha | `var(--awb-color1)` | Info box text color |
| `map_custom_marker_icon` | textarea | empty | Custom marker icon URLs (use \| for multiple, or "theme") |

---

## 27. Performance

### General

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `lazy_load` | radio-buttonset | `none` | Image lazy loading. Choices: avada, wordpress, none |
| `lazy_load_iframes` | radio-buttonset | `none` | Iframe lazy loading. Choices: avada, wordpress, none |
| `font_face_display` | radio-buttonset | `block` | Font rendering. Choices: block (clean render, slower), swap (faster, FOUT), swap-all (swap everything) |
| `preload_fonts` | radio-buttonset | `icon_fonts` | Font preloading. Choices: all, google_fonts, icon_fonts, none |
| `preload_fonts_variants` | select (multi) | `400` | Google font variants to preload |
| `preload_fonts_subsets` | select (multi) | `latin` | Google font subsets to preload |
| `emojis_disabled` | radio-buttonset | `enabled` | WordPress emojis script. Choices: enabled, disabled |
| `jquery_migrate_disabled` | radio-buttonset | `enabled` | jQuery Migrate script. Choices: enabled, disabled |
| `defer_jquery` | switch | `0` | Load jQuery in footer (use with caution) |
| `defer_styles` | switch | `0` | Load stylesheets in footer (may cause FOUC) |
| `gzip_status` | switch | `0` | Enable Gzip compression (.htaccess, Apache only) |
| `video_facade` | radio-buttonset | `off` | Video facade (load player on play). Choices: on, off |
| `clear_object_cache` | switch | `0` | Clear WP object cache on post edit |

### Images

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `svg_upload` | radio-buttonset | `disabled` | SVG media upload. Choices: enabled, disabled |
| `upload_image_format` | radio-buttonset | `default` | Upload image format. Choices: default, webp, avif |
| `keep_original_images` | radio-buttonset | `disable` | Keep original format images. Choices: enable, disable |
| `display_image_format` | radio-buttonset | `modern` | Display image format. Choices: modern, original |
| `pw_jpeg_quality` | slider | `82` | JPEG image quality (1-100) |
| `webp_image_quality` | slider | `86` | WebP image quality (1-100) |
| `awb_image_sizes` | select (multi) | all sizes | Avada image sizes to generate |
| `wp_big_image_size_threshold` | slider | `2560` | Max image dimension threshold (0=disabled, max 5000) |

### Dynamic CSS & JS

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `css_cache_method` | radio-buttonset | `file` | CSS compile method. Choices: file, db, off |
| `css_combine_third_party_assets` | select (multi) | `[]` | Combine third-party CSS. Choices: tec, slider_rev, convert_plus, contact_form_7, bbpress |
| `media_queries_async` | switch | `0` | Load media queries async |
| `critical_css` | switch | `0` | Enable critical CSS generation |
| `cache_server_ip` | text | empty | Cache server IP (for Varnish + CloudFlare) |
| `js_compiler` | switch | `1` | Enable JS compiler (combining) |

### Progressive Web App (PWA)

Requires the PWA plugin.

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `pwa_enable` | switch | `0` | Enable Progressive Web App |
| `pwa_filetypes_cache_first` | select (multi) | images,scripts,styles,fonts | Cache-first strategy file types |
| `pwa_filetypes_network_first` | select (multi) | `[]` | Network-first strategy file types |
| `pwa_filetypes_stale_while_revalidate` | select (multi) | `[]` | Stale-while-revalidating file types |
| `pwa_manifest_logo` | media | empty | App splash screen logo (512x512, PNG) |
| `pwa_manifest_display` | select | `minimal-ui` | App display mode. Choices: fullscreen, standalone, minimal-ui, browser |
| `pwa_theme_color` | color | `#ffffff` | App theme color / toolbar color |

---

## 28. Privacy

### General

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `gfonts_load_method` | radio-buttonset | `cdn` | Google/FontAwesome fonts loading. Choices: local (GDPR-friendly), cdn |
| `privacy_embeds` | switch | `0` | Require consent before loading embeds/scripts |
| `privacy_expiry` | slider | `30` | Consent cookie expiration in days (1-366) |
| `privacy_embed_types` | select (multi) | all types | Types of embeds requiring consent |
| `privacy_embed_defaults` | select (multi) | `[]` | Types checked by default |
| `privacy_bg_color` | color-alpha | AWB color8 10% | Privacy placeholder background |
| `privacy_color` | color-alpha | AWB color8 30% | Privacy placeholder text color |

### Privacy Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `privacy_bar` | switch | `0` | Enable privacy bar at bottom |
| `privacy_bar_padding` | spacing | `15px 30px` | Privacy bar padding |
| `privacy_bar_bg_color` | color-alpha | `var(--awb-color8)` | Bar background color |
| `privacy_bar_font_size` | dimension | `13px` | Bar font size |
| `privacy_bar_color` | color-alpha | `var(--awb-color6)` | Bar text color |
| `privacy_bar_link_color` | color-alpha | `var(--awb-color2)` | Bar link color |
| `privacy_bar_link_hover_color` | color-alpha | `var(--awb-color4)` | Bar link hover color |
| `privacy_bar_text` | textarea | Cookie notice text | Bar text content |
| `privacy_bar_button_text` | text | `OK` | Accept button text |
| `privacy_bar_button_save` | switch | `0` | Save default consent on button click |
| `privacy_bar_more` | switch | `0` | Show settings section |
| `privacy_bar_more_text` | text | `Settings` | Settings link text |
| `privacy_bar_update_text` | text | `Update Settings` | Update button text |
| `privacy_bar_headings_font_size` | dimension | `13px` | Settings heading font size |
| `privacy_bar_headings_color` | color-alpha | `var(--awb-color1)` | Settings heading color |
| `privacy_bar_content` | repeater | `[]` | Settings content columns (type: custom/tracking/embeds, title, description) |
| `privacy_bar_reject` | switch | `0` | Show reject button |
| `privacy_bar_reject_text` | text | `Reject` | Reject button text |

---

## 29. Maintenance Mode

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `maintenance_mode` | radio-buttonset | `off` | Mode. Choices: off, maintenance (503), coming_soon (200) |
| `maintenance_redirect_url` | text | empty | Redirect URL (overrides template) |
| `maintenance_template` | select | `0` | Maintenance page template (from published pages) |
| `maintenance_user_roles` | select (multi) | `[]` | Bypass user roles (always: admin) |
| `maintenance_exclude` | textarea | empty | Excluded URL patterns (one per line) |
| `maintenance_page_title` | text | `Maintenance` | Browser page title |
| `maintenance_robots_meta` | radio-buttonset | `noindex` | Robots meta. Choices: noindex, index |

---

## 30. Advanced / Features

### Theme Features

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `enable_language_updates` | switch | `1` | Enable language file updates |
| `dependencies_status` | switch | `1` | Enable dependencies system |
| `disable_code_block_encoding` | switch | `0` | Disable code block auto-encoding |
| `disable_megamenu` | switch | `0` | Disable mega menu |
| `status_widget_areas` | switch | `1` | Enable custom widget areas |
| `status_avada_studio` | switch | `1` | Enable Avada Studio |
| `avada_rev_styles` | switch | `1` | Load Avada Slider Revolution styles |
| `avada_styles_dropdowns` | switch | `1` | Load Avada dropdown styles |
| `disable_mobile_image_hovers` | switch | `1` | Disable mobile image hover animations |

### APIs & External Scripts

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `status_yt` | switch | `1` | Enable YouTube script |
| `status_vimeo` | switch | `1` | Enable Vimeo script |
| `status_gmap` | switch | `1` | Enable Google Maps script |
| `status_fontawesome` | select (multi) | all subsets | Font Awesome subsets. Choices: fab (brands), far (regular), fas (solid), fal (light) |
| `fontawesome_v4_compatibility` | switch | `0` | Font Awesome v4 compatibility |
| `status_fontawesome_pro` | switch | `0` | Enable Font Awesome Pro |
| `status_outline` | switch | `0` | Enable Outline icon subset |

### SEO / Meta Tags

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `meta_tags_separator` | text | `\|` | Meta tags separator character |
| `status_opengraph` | switch | `1` | Enable Open Graph meta tags |
| `disable_date_rich_snippet_pages` | switch | `0` | Disable date rich snippet on pages |
| `disable_rich_snippet_title` | switch | `0` | Disable rich snippet title |
| `disable_rich_snippet_author` | switch | `0` | Disable rich snippet author |
| `disable_rich_snippet_date` | switch | `0` | Disable rich snippet date |
| `disable_rich_snippet_faq` | switch | `0` | Disable FAQ rich snippet |

### Block Editor

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `enable_block_editor_backend_styles` | switch | `1` | Backend block styles |
| `load_block_styles` | radio-buttonset | `auto` | Frontend block styles. Choices: auto, on, off |

### Code Injection

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `google_analytics` | code | empty | Tracking code (analytics, tag manager) |
| `space_head` | code | empty | Code before `</head>` |
| `space_body_open` | code | empty | Code after opening `<body>` |
| `space_body` | code | empty | Code before `</body>` |

### Post Types

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `status_fusion_slider` | switch | `1` | Enable Avada Slider post type |
| `status_eslider` | switch | `1` | Enable Elastic Slider post type |
| `status_fusion_forms` | switch | `1` | Enable Avada Forms post type |
| `status_awb_Off_Canvas` | switch | `1` | Enable Off Canvas post type |
| `status_fusion_portfolio` | switch | `1` | Enable Portfolio post type |
| `status_fusion_faqs` | switch | `1` | Enable FAQ post type |

---

## 31. Custom CSS

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `custom_css` | code | empty | Custom CSS code (no `<style>` tags needed, auto-encoded) |

---

## 32. Custom Auth Pages

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `auth_pages_login_page` | select | `0` (WP Default) | Custom login page |
| `auth_pages_registration_page` | select | `0` (WP Default) | Custom registration page |
| `auth_pages_lost_password_page` | select | `0` (WP Default) | Custom lost password page |
| `auth_pages_reset_password_page` | select | `0` (WP Default) | Custom reset password page |
| `auth_pages_custom_redirect` | select | `auth_pages` | WP auth page redirect. Choices: auth_pages, homepage, 404, custom_page |
| `auth_pages_custom_redirect_page` | select | `0` | Custom redirect page |
| `auth_pages_bypass_param` | text | empty | Query parameter to bypass custom auth |

---

## 33. Page-Level Overrides (Post Meta)

Avada allows per-page option overrides using post meta with `pyre_` prefix. The actual DB meta key is `_fusion_builder_[field_id]`, but the admin field uses `pyre_[field_id]` as HTML ID. Set via `mcm/update-content`:

```json
mcm/update-content {"id": <page_id>, "meta": {"pyre_header_bg_color": "#FF0000"}}
```

### Page Options

| Meta Key | Type | Description |
|----------|------|-------------|
| `pyre_page_bg_layout` | radio-buttonset | Page layout (wide/boxed/default) |
| `pyre_page_bg_color` | color-alpha | Page background color |
| `pyre_page_bg` | media | Page background image |
| `pyre_page_bg_full` | radio-buttonset | Full background image (yes/no) |
| `pyre_page_bg_repeat` | select | Background repeat (repeat/repeat-x/repeat-y/no-repeat) |
| `pyre_content_bg_color` | color-alpha | Content background color |
| `pyre_main_top_padding` | dimension | Main content top padding |
| `pyre_main_bottom_padding` | dimension | Main content bottom padding |
| `pyre_sidebar_position` | radio-buttonset | Sidebar position (left/right/default) |
| `pyre_sidebar_bg_color` | color-alpha | Sidebar background color |
| `pyre_container_hundred_percent_animation` | select | 100% width scroll animation |
| `pyre_container_hundred_percent_scroll_sensitivity` | slider | Scroll sensitivity |
| `pyre_container_hundred_percent_animation_speed` | slider | Animation speed |

### Header Page Options

| Meta Key | Type | Description |
|----------|------|-------------|
| `pyre_display_header` | radio-buttonset | Show/hide header (yes/no) |
| `pyre_header_100_width` | radio-buttonset | 100% width header (yes/no) |
| `pyre_header_bg_color` | color-alpha | Page header background color |
| `pyre_mobile_header_bg_color` | color-alpha | Mobile header background color |
| `pyre_header_bg_image` | media | Header background image |
| `pyre_header_bg_full` | radio-buttonset | Full header background (yes/no) |
| `pyre_header_bg_repeat` | select | Header bg repeat |
| `pyre_displayed_menu` | select | Override menu for this page |

### Page Title Bar Options

| Meta Key | Type | Description |
|----------|------|-------------|
| `pyre_page_title_bar` | radio-buttonset | Page title bar (bar_and_content/content_only/hide/default) |
| `pyre_page_title_text` | radio-buttonset | Show page title text (yes/no/default) |
| `pyre_page_title_bar_bs` | radio-buttonset | Below title bar content (default/breadcrumbs/search_box/none) |
| `pyre_page_title` | text | Custom page title text |
| `pyre_page_title_custom_subheader` | textarea | Custom page subtitle |
| `pyre_page_title_bg_color` | color-alpha | Page title bar background color |
| `pyre_page_title_text_color` | color-alpha | Page title text color |
| `pyre_page_title_height` | dimension | Page title bar height |
| `pyre_page_title_bg` | media | Page title background image URL |
| `pyre_page_title_bg_full` | radio-buttonset | Full background image (yes/no) |
| `pyre_page_title_bg_parallax` | radio-buttonset | Parallax background (yes/no) |
| `pyre_page_title_breadcrumbs_search_bar` | radio-buttonset | Breadcrumbs/search bar (default/breadcrumbs/search_box/none) |

### Slider Page Options

| Meta Key | Type | Description |
|----------|------|-------------|
| `pyre_slider_type` | select | Page slider type (no, flex, flex2, rev, elastic, layer) |
| `pyre_slider_position` | radio-buttonset | Slider position (above/below header) |

### Footer Page Options

| Meta Key | Type | Description |
|----------|------|-------------|
| `pyre_display_footer` | radio-buttonset | Show/hide footer (yes/no) |
| `pyre_display_copyright` | radio-buttonset | Show/hide copyright bar (yes/no) |

---

## Notes for Shortcode Styling

Avada Builder element styling options have been moved to the Avada Builder Elements options panel (separate from `fusion_options`). They are not part of the theme options and cannot be configured via `mcm/set-theme-options`.

---

## Summary Count

| Category | Sections | Approx. Options |
|----------|----------|-----------------|
| Colors & Typography | 2 | ~38 |
| Header & Navigation | 4 | ~110 |
| Page Title & Breadcrumbs | 2 | ~32 |
| Footer & Copyright | 3 | ~30 |
| Sliding Bar & Sidebars | 2 | ~60 |
| Blog & Portfolio | 4 | ~80 |
| Search & Social | 2 | ~35 |
| WooCommerce | 1 | ~60 |
| Integrations (EC/bbP) | 2 | ~30 |
| Layout & Background | 2 | ~18 |
| Logo | 1 | ~14 |
| Responsive | 1 | ~10 |
| Slideshows & Sliders | 2 | ~17 |
| Lightbox | 1 | ~19 |
| Forms | 1 | ~25 |
| Extra / Miscellaneous | 1 | ~50 |
| Contact Template | 1 | ~25 |
| Performance | 1 | ~35 |
| Privacy | 1 | ~25 |
| Maintenance | 1 | ~7 |
| Advanced / Features | 1 | ~30 |
| Custom CSS & Auth | 2 | ~8 |
| Page-Level Overrides | 1 | ~40 |
| **TOTAL** | **33** | **~630+** |
