# Avada — Configurable Options

All options are stored in `wp_options` table as a serialized array under option name `fusion_options`. Read via `mcm/get-theme-options` and update via `mcm/set-theme-options` (auto-detects `fusion_options` for Avada).

---

## Colors

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `color_palette` | color-palette | AWB defaults | Global color palette (8 core colors) |
| `primary_color` | color-alpha | `var(--awb-color5)` | Primary accent color |

### AWB Global Color Variables

Avada 7.x+ uses CSS custom properties for its color palette:

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

## Typography

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `typography_sets` | typography-sets | AWB defaults | Global typography presets |
| `body_typography` | typography | Font vars | Body text font settings |
| `h1_typography` | typography | 64px | Heading 1 font settings |
| `h2_typography` | typography | AWB var | Heading 2 font settings |
| `h3_typography` | typography | 36px | Heading 3 font settings |
| `h4_typography` | typography | 24px | Heading 4 font settings |
| `h5_typography` | typography | 20px | Heading 5 font settings |
| `h6_typography` | typography | 16px | Heading 6 font settings |
| `post_title_typography` | typography | 48px | Post title font settings |
| `post_titles_extras_typography` | typography | 20px | Post subtitle/extras font |
| `link_color` | color-alpha | `var(--awb-color8)` | Link color |
| `link_hover_color` | color-alpha | `var(--awb-color5)` | Link hover color |
| `link_decoration` | switch | `0` | Enable link text decoration |
| `link_decoration_line` | select | `none` | Decoration line type |
| `link_decoration_style` | select | `solid` | Decoration line style |
| `link_decoration_thickness` | dimension | `1px` | Decoration line thickness |
| `custom_fonts` | repeater | `[]` | Custom font uploads |
| `adobe_fonts_id` | text | empty | Adobe Fonts project ID |

### Typography field structure

Typography fields are arrays with:
```php
[
    "font-family"    => "Arial, sans-serif",
    "font-size"      => "16px",
    "font-weight"    => "400",
    "line-height"    => "1.6",
    "letter-spacing" => "0",
    "font-style"     => "normal",
    "text-transform" => "none",
    "color"          => "#333333"
]
```

---

## Header

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header_position` | radio-buttonset | `top` | Header position (top/left/right) |
| `header_layout` | radio-image | `v3` | Header layout version (v1-v7) |
| `slider_position` | radio-buttonset | `below` | Slider above/below header |
| `header_left_content` | select | `social_links` | Left header area content |
| `header_right_content` | select | `navigation` | Right header area content |
| `header_v4_content` | select | `tagline_and_search` | V4 header content type |
| `header_bg_color` | color-alpha | `var(--awb-color1)` | Header background color |
| `header_bg_image` | media | empty | Header background image |
| `header_bg_full` | switch | `0` | Full-width header bg image |
| `header_bg_parallax` | switch | `1` | Parallax header bg |
| `header_border_color` | color-alpha | transparent | Header border color |
| `header_shadow` | switch | `0` | Header shadow |
| `header_100_width` | switch | `0` | 100% width header |
| `header_padding` | spacing | `0px` all | Header padding |
| `side_header_width` | slider | `280` | Side header width (px) |
| `header_number` | text | Phone number | Contact number in header |
| `header_email` | text | Email | Contact email in header |
| `header_tagline` | textarea | Tagline text | Header tagline |
| `header_banner_code` | code | empty | Header banner HTML |

### Sticky Header

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header_sticky` | switch | `1` | Enable sticky header |
| `header_sticky_tablet` | switch | `0` | Sticky on tablet |
| `header_sticky_mobile` | switch | `0` | Sticky on mobile |
| `header_sticky_shrinkage` | switch | `0` | Shrink on scroll |
| `header_sticky_shadow` | switch | `1` | Sticky header shadow |
| `header_sticky_bg_color` | color-alpha | `var(--awb-color1)` | Sticky bg color |
| `header_sticky_menu_color` | color-alpha | `var(--awb-color8)` | Sticky menu text color |
| `header_sticky_nav_padding` | slider | `35` | Sticky nav padding |
| `header_sticky_nav_font_size` | dimension | `14px` | Sticky nav font size |
| `header_sticky_type2_layout` | radio-buttonset | `menu_only` | Sticky layout type |

### Top Header Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header_top_bg_color` | color-alpha | `var(--awb-color4)` | Top bar background |
| `archive_header_bg_color` | color-alpha | `var(--awb-color1)` | Archive header bg |
| `tagline_font_size` | dimension | `16px` | Tagline font size |
| `tagline_font_color` | color-alpha | `var(--awb-color8)` | Tagline text color |

---

## Footer

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `footer_widgets` | switch | `1` | Show footer widgets |
| `footer_widgets_columns` | slider | `4` | Number of widget columns |
| `footer_widgets_center_content` | switch | `0` | Center widget content |
| `footer_copyright` | switch | `1` | Show copyright bar |
| `footer_copyright_center_content` | switch | `0` | Center copyright |
| `footer_text` | code | Template | Copyright HTML |
| `footer_100_width` | switch | `0` | Full-width footer |
| `footer_special_effects` | radio | `none` | Footer special effects |
| `footer_bg_color` | color-alpha | `var(--awb-color7)` | Footer background |
| `footer_border_size` | slider | `0` | Footer border size |
| `footer_border_color` | color-alpha | `var(--awb-color3)` | Footer border color |
| `footer_divider_line` | switch | `0` | Footer divider line |
| `footer_divider_line_size` | slider | `1` | Divider thickness |
| `footer_divider_line_style` | select | `solid` | Divider style |
| `footer_divider_color` | color-alpha | `var(--awb-color6)` | Divider color |
| `footer_area_padding` | spacing | `60px 0 64px 0` | Footer area padding |
| `footer_widgets_padding` | dimension | `16px` | Widget spacing |
| `footer_headings_typography` | typography | weight 600 | Footer heading font |
| `footer_text_color` | color-alpha | color1 opacity | Footer text color |
| `footer_link_color` | color-alpha | color1 reduced | Footer link color |
| `footer_link_color_hover` | color-alpha | `var(--awb-color4)` | Footer link hover |

### Footer Background

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `footerw_bg_image` | media | empty | Footer bg image |
| `footerw_bg_full` | switch | `0` | Full-width footer bg |
| `footerw_bg_repeat` | select | `no-repeat` | BG image repeat |
| `footerw_bg_pos` | select | `center center` | BG image position |

### Copyright Bar

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `copyright_padding` | spacing | `20px 0` | Copyright padding |
| `copyright_bg_color` | color-alpha | `var(--awb-color8)` | Copyright bg color |
| `copyright_border_size` | slider | `0` | Copyright border |
| `copyright_border_color` | color-alpha | `var(--awb-color8)` | Copyright border color |
| `copyright_text_color` | color-alpha | reduced opacity | Copyright text |
| `copyright_link_color` | color-alpha | reduced opacity | Copyright link |
| `copyright_link_color_hover` | color-alpha | `var(--awb-color4)` | Copyright link hover |
| `copyright_font_size` | dimension | `13px` | Copyright font size |

---

## Layout

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `layout` | radio-buttonset | `wide` | Site layout (wide/boxed) |
| `site_width` | dimension | `1200px` | Maximum site width |
| `margin_offset` | spacing | `0px 0` | Site margin offset |
| `scroll_offset` | radio-buttonset | `full` | Scroll offset behavior |
| `boxed_modal_shadow` | select | `none` | Boxed layout shadow |
| `main_padding` | spacing | `60px 0` | Main content padding |
| `page_template` | radio-buttonset | `100_width` | Default page template |
| `hundredp_padding` | dimension | `30px` | 100% width padding |

---

## Background

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `bg_color` | color-alpha | `var(--awb-color3)` | Body background color |
| `bg_image` | media | empty | Body background image |
| `bg_full` | switch | `0` | Full-screen body bg |
| `bg_repeat` | select | `no-repeat` | Body bg repeat |
| `bg_pattern_option` | switch | `0` | Use pattern bg |
| `bg_pattern` | radio-image | `pattern1` | Pattern selection |
| `content_bg_color` | color-alpha | `var(--awb-color1)` | Content area bg color |
| `content_bg_image` | media | empty | Content bg image |
| `content_bg_full` | switch | `0` | Full content bg |
| `content_bg_repeat` | select | `no-repeat` | Content bg repeat |

---

## Logo

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `logo` | media | Avada logo | Main logo |
| `logo_retina` | media | Avada retina | Retina logo |
| `sticky_header_logo` | media | empty | Sticky header logo |
| `sticky_header_logo_retina` | media | empty | Sticky retina logo |
| `mobile_logo` | media | empty | Mobile logo |
| `mobile_logo_retina` | media | empty | Mobile retina logo |
| `logo_alignment` | radio-buttonset | `left` | Logo alignment |
| `logo_margin` | spacing | `34px 0` | Logo margin |
| `logo_background` | switch | `0` | Logo background |
| `logo_background_color` | color-alpha | `var(--awb-color4)` | Logo bg color |
| `logo_custom_link` | text | empty | Custom logo link |
| `fav_icon` | media | empty | Favicon |
| `fav_icon_apple_touch` | media | empty | Apple touch icon |
| `fav_icon_android` | media | empty | Android icon |

---

## Menu / Navigation

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `nav_height` | slider | `94` | Navigation height (px) |
| `menu_highlight_style` | radio-buttonset | `bar` | Menu highlight style |
| `menu_highlight_background` | color-alpha | `var(--awb-color4)` | Highlight bg color |
| `nav_highlight_border` | slider | `3` | Highlight border size |
| `nav_padding` | slider | `48` | Nav item padding |
| `mobile_nav_padding` | slider | `25` | Mobile nav padding |
| `menu_arrow_size` | dimensions | `23x12` | Dropdown arrow size |
| `megamenu_shadow` | switch | — | Mega menu shadow |

---

## Blog

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `blog_title` | text | `Blog` | Blog page title |
| `blog_subtitle` | text | empty | Blog subtitle |
| `blog_layout` | select | `large` | Blog layout type |
| `blog_archive_layout` | select | `large` | Archive layout |
| `blog_pagination_type` | radio-buttonset | `pagination` | Pagination type |
| `blog_archive_grid_columns` | slider | `3` | Grid columns |
| `blog_archive_grid_column_spacing` | slider | `40` | Grid spacing |
| `blog_equal_heights` | switch | `0` | Equal height cards |
| `blog_layout_alignment` | radio-buttonset | empty | Content alignment |
| `content_length` | radio-buttonset | `excerpt` | Content display |
| `excerpt_length_blog` | slider | `10` | Excerpt word count |
| `strip_html_excerpt` | switch | `1` | Strip HTML from excerpts |
| `featured_images` | switch | `1` | Show featured images |
| `featured_images_single` | switch | `1` | Featured on single posts |
| `blog_width_100` | switch | `0` | 100% width blog |
| `blog_pn_nav` | switch | `1` | Previous/next navigation |
| `blog_post_title` | radio-buttonset | `below` | Post title position |
| `blog_post_meta_position` | radio-buttonset | `below_article` | Meta position |
| `social_sharing_box` | switch | `1` | Show social sharing |
| `author_info` | switch | `1` | Show author info |
| `related_posts` | switch | `1` | Show related posts |
| `blog_comments` | switch | `1` | Show comments |
| `post_meta` | switch | `1` | Show post meta |
| `post_meta_author` | switch | `1` | Show author in meta |
| `post_meta_date` | switch | `1` | Show date in meta |
| `post_meta_cats` | switch | `1` | Show categories |
| `post_meta_comments` | switch | `1` | Show comment count |
| `post_meta_read` | switch | `1` | Show read more |
| `post_meta_tags` | switch | `0` | Show tags |
| `meta_font_size` | dimension | `13px` | Meta font size |
| `date_format` | text | empty | Custom date format |
| `dates_box_color` | color-alpha | `var(--awb-color2)` | Date box color |

### Blog Load More

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `blog_load_more_posts_button_bg_color` | color-alpha | `var(--awb-color7)` | Load more bg |
| `blog_load_more_posts_button_text_color` | color-alpha | `var(--awb-color1)` | Load more text |
| `blog_load_more_posts_hover_button_bg_color` | color-alpha | `var(--awb-color5)` | Load more hover bg |
| `blog_load_more_posts_hover_button_text_color` | color-alpha | `var(--awb-color1)` | Load more hover text |

---

## WooCommerce

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `woo_items` | slider | `12` | Products per page |
| `woocommerce_shop_page_columns` | slider | `4` | Shop columns |
| `woocommerce_related_columns` | slider | `4` | Related products columns |
| `woocommerce_archive_page_columns` | slider | `3` | Archive columns |
| `woocommerce_archive_grid_column_spacing` | slider | `40` | Archive grid spacing |
| `woocommerce_product_images_layout` | radio-buttonset | `avada` | Product image layout |
| `woocommerce_product_images_zoom` | switch | `1` | Image zoom |
| `woocommerce_single_gallery_size` | dimension | `500px` | Gallery size |
| `woocommerce_gallery_thumbnail_width` | slider | `200` | Thumbnail width |
| `woocommerce_gallery_thumbnail_columns` | slider | `4` | Thumbnail columns |
| `woocommerce_product_images_thumbnail_position` | radio-buttonset | `bottom` | Thumbnail position |
| `woocommerce_enable_quick_view` | switch | `0` | Quick view |
| `woocommerce_variations` | switch | `1` | Show variations |
| `woocommerce_avada_ordering` | switch | `1` | Custom ordering |
| `woocommerce_disable_crossfade_effect` | switch | `1` | Disable crossfade |
| `woocommerce_one_page_checkout` | switch | `0` | One-page checkout |
| `woocommerce_enable_order_notes` | switch | `1` | Order notes |
| `woocommerce_acc_link_main_nav` | switch | `0` | Account link in nav |
| `woocommerce_cart_link_main_nav` | switch | `1` | Cart link in nav |
| `woocommerce_cart_counter` | switch | `0` | Cart counter badge |
| `woocommerce_cart_link_top_nav` | switch | `1` | Cart in top nav |

---

## Responsive

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `responsive` | radio-buttonset | `1` | Enable responsive |
| `grid_main_break_point` | slider | `1000` | Main breakpoint (px) |
| `side_header_break_point` | slider | `800` | Side header breakpoint |
| `content_break_point` | slider | `800` | Content breakpoint |
| `sidebar_break_point` | slider | `800` | Sidebar breakpoint |
| `mobile_zoom` | switch | `1` | Allow mobile zoom |
| `visibility_small` | slider | `640` | Small screen max (px) |
| `visibility_medium` | slider | `1024` | Medium screen max (px) |
| `typography_sensitivity` | slider | `0` | Responsive typography |
| `typography_factor` | slider | `1.5` | Typography scale factor |

---

## Page-Level Overrides (Post Meta)

Avada allows per-page overrides using post meta with `pyre_` prefix:

| Meta Key | Description |
|----------|-------------|
| `pyre_header_bg_color` | Page header background |
| `pyre_slider_type` | Page slider type |
| `pyre_display_header` | Show/hide header |
| `pyre_display_footer` | Show/hide footer |
| `pyre_page_bg_color` | Page background color |
| `pyre_sidebar_position` | Sidebar position |
| `pyre_page_title_bar` | Page title bar |

```json
// Set page-level override via mcm/update-content
mcm/update-content {"id": <page_id>, "meta": {"pyre_header_bg_color": "#FF0000"}}
```
