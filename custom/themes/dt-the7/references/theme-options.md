# The7 — Configurable Options

All options are stored in `wp_options` table as a serialized array under option name `the7mk2`. Read via `mcm/get-theme-options` and update via `mcm/set-theme-options` (auto-detects `the7mk2` for The7).

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

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `general-accent_color_mode` | radio | `color` | Accent mode (color/gradient) |
| `general-accent_bg_color` | color | `#D73B37` | Accent color |
| `general-accent_bg_color_gradient` | gradient | `45deg\|...` | Accent gradient |
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

---

## Typography / Fonts

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `fonts-font_family` | web_fonts | `Arial` | Body font family |
| `fonts-big_size` | font_sizes | — | Large text sizes |
| `fonts-normal_size` | font_sizes | — | Normal text sizes |
| `fonts-small_size` | font_sizes | — | Small text sizes |
| `fonts-headers-font-family` | web_fonts | — | Heading font family |
| `fonts-headers-text-transform` | select | — | Heading text transform |
| `fonts-h1-typography` | typography | `44px` | H1 typography |
| `fonts-h2-typography` | typography | `26px` | H2 typography |
| `fonts-h3-typography` | typography | `22px` | H3 typography |
| `fonts-h4-typography` | typography | `18px` | H4 typography |
| `fonts-h5-typography` | typography | `15px` | H5 typography |
| `fonts-h6-typography` | typography | `12px` | H6 typography |
| `fonts-widget-title` | typography | `15px` | Widget title typography |
| `fonts-widget-content` | typography | `13px` | Widget content typography |
| `widget_gap` | number | `15px` | Widget gap/spacing |

---

## Branding / Logo

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-logo-padding` | spacing | `0px 0px 0px 0px` | Main logo padding |
| `header-style-transparent-choose_logo` | radio | `custom` | Transparent header logo source |
| `header-style-transparent-logo-padding` | spacing | `0px` all | Transparent logo padding |
| `header-style-floating-choose_logo` | radio | `custom` | Floating header logo source |
| `header-style-floating-logo-padding` | spacing | `0px` all | Floating logo padding |
| `header-mobile-first_switch-logo` | radio | `mobile` | Mobile logo (1st breakpoint) |
| `header-mobile-second_switch-logo` | radio | `mobile` | Mobile logo (2nd breakpoint) |
| `header-style-mobile-logo-padding` | spacing | `0px` all | Mobile logo padding |
| `general-favicon` | upload | — | Favicon |
| `general-favicon_hd` | upload | — | Retina favicon |
| `general-handheld_icon-old_iphone` | upload | — | iPhone icon |
| `general-handheld_icon-old_ipad` | upload | — | iPad icon |
| `general-handheld_icon-retina_iphone` | upload | — | Retina iPhone icon |
| `general-handheld_icon-retina_ipad` | upload | — | Retina iPad icon |

---

## Footer

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `footer-style` | images | `content_width_line` | Footer style |
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
| `general-title_decoration` | radio | `none` | Title decoration |
| `general-show_breadcrumbs` | images | `1` | Show breadcrumbs |
| `breadcrumbs-typography` | typography | — | Breadcrumb typography |
| `general-breadcrumbs_color` | color | `#ffffff` | Breadcrumb color |
| `breadcrumbs_padding` | spacing | `3px 12px 2px 12px` | Breadcrumb padding |
| `breadcrumbs_margin` | spacing | `0px` all | Breadcrumb margin |
| `breadcrumbs_bg_color` | alpha_color | `rgba(255,255,255,0.2)` | Breadcrumb bg color |
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

## Header

| Option ID | Type | Default | Description |
|-----------|------|---------|-------------|
| `header-background` | images | `normal` | Header bg mode (normal/transparent) |
| `header-transparent_bg_color` | alpha_color | `rgba(0,0,0,0.5)` | Transparent header bg |
| `top-bar-transparent_bg_color` | alpha_color | `rgba(0,0,0,0.5)` | Transparent top bar bg |

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
| `buttons-color_mode` | radio | `accent` | Button color mode |
| `buttons-color` | alpha_color | `#ffffff` | Button custom color |
| `buttons-color_gradient` | gradient | — | Button gradient |
| `buttons-hover_color_mode` | radio | `accent` | Hover color mode |
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
| `sidebar-decoration` | images | `none` | Sidebar decoration |
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
| `contact_form_recaptcha_site_key` | text | — | reCAPTCHA site key |
| `contact_form_recaptcha_secret_key` | password | — | reCAPTCHA secret key |

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
