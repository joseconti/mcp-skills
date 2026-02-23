---
name: avada
description: "Use when configuring the Avada WordPress theme (ThemeFusion). Guides the user through a 5-phase conversation to fully configure Avada — covering ALL 600+ options across 33 sections (colors, typography, header, footer, page title bar, breadcrumbs, sliding bar, sidebars, blog, portfolio, search, social media, WooCommerce, Events Calendar, bbPress, layout, background, logo, responsive, slideshows, elastic slider, lightbox, forms, extra, contact, performance, privacy, maintenance, advanced, custom CSS, auth pages, and page-level overrides). Classic theme — options stored in wp_options as fusion_options. Logo uses both Avada options AND WordPress custom_logo theme mod."
compatibility: "Avada 7.14+. Requires WordPress 4.9+ and PHP 5.6+. Classic theme (NOT FSE)."
---

# Avada Theme Configuration

## Theme Type

**Classic theme (NOT Full Site Editing)**. Configuration is split between three storage mechanisms:

1. **Theme options** (`fusion_options` in `wp_options`): All visual styling — colors, typography, header, footer, layout, blog, portfolio, search, social media, WooCommerce, lightbox, forms, performance, privacy, maintenance, and more. Read/write via `mcm/get-theme-options` and `mcm/set-theme-options`.
2. **Theme mods** (`theme_mods_Avada` in `wp_options`): `custom_logo` (attachment ID), navigation menu locations. Read/write via `mcm/get-theme-mod` and `mcm/set-theme-mod`.
3. **Page-level overrides** (post meta): Per-page settings with `pyre_` prefix. Read/write via `mcm/update-content`.

Does NOT use Global Styles or theme.json.

## When to use

- The user wants to change colors, fonts, header, footer, or layout of Avada
- The user wants to configure blog, portfolio, search, or social media settings
- The user wants to set up WooCommerce shop styling
- The user wants to adjust page title bar, breadcrumbs, or sliding bar
- The user wants to configure sidebars and widget areas
- The user wants to set up logo, favicons, and branding
- The user wants to configure lightbox, forms, or privacy settings
- The user wants to adjust responsive breakpoints or performance settings
- The user wants to set up maintenance mode or custom auth pages
- The user wants to set up the site identity
- The user wants to inject custom CSS or tracking code
- The user wants to configure page-level overrides

## Inputs required

- What aspect to configure (specific area, or "all" for full setup)
- The desired values (specific colors, font choices, sizes, etc.)

---

## 5-Phase Configuration Flow

When configuring Avada, guide the user through progressive phases. Each phase groups related options. **Always explain what each option controls** so the user can make informed decisions. Use the three-tier system:

- **Essential** (~35 options): Always ask — site identity, logo, primary colors, header layout, footer basics, body font
- **Recommended** (~120 options): Ask during full setup — all color details, typography, blog, WooCommerce, responsive, page title bar, sidebars, social media
- **Advanced** (~300 options): Only ask when the user requests fine-tuning — breadcrumb colors, sliding bar, search settings, portfolio archive details, lightbox, forms, performance, code injection, post type toggles, maintenance, privacy bar, elastic slider

---

### Phase 1: FOUNDATION (Always run this phase)

#### 1.1 Site Identity

Ask the user:
> "Let's set up the basics. What is the **site name** and **tagline** for your website? Also, do you have a **static homepage** and a **blog page** already created? If so, I'll set them as your front page and posts page."

```json
mcm/set-option {"name": "blogname", "value": "Site Name"}
mcm/set-option {"name": "blogdescription", "value": "Site Tagline"}
mcm/set-option {"name": "show_on_front", "value": "page"}
mcm/set-option {"name": "page_on_front", "value": <homepage_id>}
mcm/set-option {"name": "page_for_posts", "value": <blog_page_id>}
```

#### 1.2 Logo (CRITICAL — TWO places)

Ask the user:
> "Do you have a **logo** ready? I'll need the image URL. Avada uses logos in multiple places — main logo, retina (high-resolution) version, mobile logo, and sticky header logo. At minimum I need the **main logo**. Do you also have retina and mobile versions?"

Avada stores logos as **URLs** in `fusion_options` AND as **attachment ID** in `custom_logo` theme mod. Always set BOTH:

```json
// Step 1: Upload
mcm/upload-media {"url": "https://example.com/logo.png", "title": "Site Logo"}
// → Returns: attachment_id and url

// Step 2: Set in Avada options (URL format)
mcm/set-theme-options {"values": {"logo": {"url": "<uploaded_url>"}}}

// Step 3: Set WordPress theme mod (attachment ID)
mcm/set-theme-mod {"key": "custom_logo", "value": <attachment_id>}

// Step 4: Set retina/mobile/sticky if provided
mcm/set-theme-options {"values": {
  "logo_retina": {"url": "<retina_url>"},
  "mobile_logo": {"url": "<mobile_url>"},
  "sticky_header_logo": {"url": "<sticky_url>"}
}}
```

#### 1.3 Favicon

Ask the user:
> "Do you have a **favicon** (the small icon that appears in browser tabs)? I need a square image, ideally 512x512 pixels."

```json
mcm/upload-media {"url": "https://example.com/favicon.png", "title": "Favicon"}
mcm/set-theme-options {"values": {"fav_icon": {"url": "<uploaded_url>"}}}
mcm/set-option {"name": "site_icon", "value": <attachment_id>}
```

#### 1.4 Color Palette

Ask the user:
> "Now let's define your **color palette**. Avada uses 8 global colors that are referenced across the entire site:
>
> 1. **Color 1** — Light/white color (used for backgrounds, light text)
> 2. **Color 2** — Secondary light color (subtle backgrounds, alternate areas)
> 3. **Color 3** — Light gray (borders, dividers, subtle backgrounds)
> 4. **Color 4** — Medium/accent color (highlights, active states, accents)
> 5. **Color 5** — Primary accent (main brand color, buttons, links on hover)
> 6. **Color 6** — Dark accent (secondary dark elements)
> 7. **Color 7** — Dark background (footer background, dark sections)
> 8. **Color 8** — Dark text (body text, headings)
>
> What are your brand colors? At minimum I need your **primary brand color** (Color 5) and your **dark text color** (Color 8). I can suggest sensible defaults for the rest."

Read the current palette first:
```json
mcm/get-theme-options {"keys": ["color_palette"]}
```

Then set individual colors:
```json
mcm/set-theme-options {"values": {
  "primary_color": "#E94560",
  "bg_color": "#FFFFFF",
  "content_bg_color": "#FFFFFF",
  "header_bg_color": "#FFFFFF",
  "footer_bg_color": "#1B1B1B"
}}
```

#### 1.5 Typography

Ask the user:
> "What **fonts** would you like to use? Avada supports Google Fonts, Adobe Fonts, and custom uploads. I need:
>
> - **Body font** — The main text font used for paragraphs and general content (e.g., Open Sans, Roboto, Lato)
> - **Heading font** — Used for all headings H1-H6 (e.g., Montserrat, Playfair Display, Poppins)
>
> What size should the body text be? (Default is 16px, which is recommended for readability.)
> Do you also want specific link colors?"

Typography fields MUST be arrays with ALL properties:
```json
mcm/set-theme-options {"values": {
  "body_typography": {
    "font-family": "Open Sans",
    "font-size": "16px",
    "font-weight": "400",
    "line-height": "1.6",
    "letter-spacing": "0",
    "font-style": "normal",
    "text-transform": "none",
    "color": "#333333"
  },
  "h1_typography": {
    "font-family": "Montserrat",
    "font-size": "48px",
    "font-weight": "700",
    "line-height": "1.2",
    "letter-spacing": "0",
    "font-style": "normal",
    "text-transform": "none",
    "color": "#252525"
  },
  "link_color": "#333333",
  "link_hover_color": "#E94560"
}}
```

To set all headings H2-H6, repeat the typography array structure for `h2_typography` through `h6_typography`.

#### 1.6 Layout

Ask the user:
> "What **layout style** do you prefer?
>
> - **Wide** (default) — Content stretches to the full browser width with a maximum width
> - **Boxed** — Content is centered in a box with visible margins on the sides
>
> What should the **maximum site width** be? (Default is 1200px. Common values: 1100px, 1200px, 1400px.)"

```json
mcm/set-theme-options {"values": {
  "layout": "wide",
  "site_width": "1200px",
  "main_padding": {"top": "60px", "bottom": "60px"}
}}
```

---

### Phase 2: STRUCTURAL (Ask before proceeding)

> "The foundation is set. Would you like to configure the **header, page structure, footer, sidebars, and sliding bar**? These control the overall structure and appearance of your site."

#### 2.1 Header

Ask the user:
> "Avada offers **7 header layout versions**:
>
> - **v1** — Logo on the left, navigation on the right (most common)
> - **v2** — Logo on the left, navigation and search on the right
> - **v3** — Logo centered between navigation items
> - **v4** — Logo on the left with search bar and tagline on the right
> - **v5** — Logo centered above the navigation menu
> - **v6** — Logo on the left, navigation in a bar below
> - **v7** — Top bar above the header with a full-width menu
>
> Which layout would you prefer? Also:
> - Should the header be at the **top**, **left side**, or **right side** of the page?
> - Do you want a **sticky header** that stays visible when scrolling?
> - Should the sticky header **shrink** when you scroll down?
> - Do you want contact info (phone/email) displayed in the header?"

```json
mcm/set-theme-options {"values": {
  "header_position": "top",
  "header_layout": "v1",
  "header_bg_color": "#FFFFFF",
  "header_border_color": "transparent",
  "header_shadow": "0",
  "header_100_width": "0",
  "header_sticky": "1",
  "header_sticky_shrinkage": "1",
  "header_sticky_bg_color": "#FFFFFF",
  "header_sticky_shadow": "1",
  "header_number": "",
  "header_email": ""
}}
```

#### 2.2 Menu / Navigation

Ask the user:
> "For the navigation menu:
> - What **height** should the menu bar be? (Default: 94px. Smaller values make the header more compact.)
> - What **highlight style** do you want for the active menu item?
>   - **Bar** — A colored bar appears above/below the active item
>   - **Arrow** — An arrow indicator points to the active item
>   - **Background** — The active item gets a colored background
> - Do you want a **search icon** in the menu? (Default: no)
> - **Dropdown menus**: What width should dropdown sub-menus be? (Default: 200px) Should dropdown items show a small arrow indicator?
> - **Mega menu**: If you have mega menus, what max width should they use? (Default: site width)
> - **Mobile menu**: What design on mobile?
>   - **Modern** — Slide-in panel with smooth animation (default)
>   - **Classic** — Collapsible accordion below the header
>   - **Flyout** — Full-screen overlay with large menu items
> - What **color** should the mobile hamburger icon be?"

```json
mcm/set-theme-options {"values": {
  "nav_height": "84",
  "menu_highlight_style": "bar",
  "nav_padding": "48",
  "main_nav_search_icon": "0",
  "menu_display_dropdown_indicator": "1",
  "dropdown_menu_width": "200px",
  "mobile_menu_design": "modern",
  "mobile_menu_toggle_color": "var(--awb-color8)"
}}
```

#### 2.3 Page Title Bar

Ask the user:
> "The **page title bar** appears at the top of each page, below the header. It typically shows the page title and optionally breadcrumbs or a search box. Options:
>
> - **Display mode**: Show the title bar with content, content only (no background bar), or hide completely
> - **Below the title**: Nothing, breadcrumbs navigation, or a search box
> - **Background**: Color, image (with optional parallax), or a fading effect on scroll
> - **Alignment**: Left, center, or right
>
> Would you like to enable the page title bar? What style do you prefer?"

```json
mcm/set-theme-options {"values": {
  "page_title_bar": "bar_and_content",
  "page_title_bar_bs": "breadcrumbs",
  "page_title_bg_color": "#F5F5F5",
  "page_title_color": "#333333",
  "page_title_font_size": "36px",
  "page_title_alignment": "left"
}}
```

#### 2.4 Breadcrumbs

If breadcrumbs are enabled in the page title bar:
> "For the **breadcrumbs** (the navigation path like Home > Blog > Post Name):
> - Do you want a **prefix text** before the breadcrumbs? (e.g., 'You are here:')
> - What **separator** between items? (Default: /)
> - Should breadcrumbs show on **mobile** devices?
> - Show the **current page name** at the end?
> - Show **post categories** in the path?"

```json
mcm/set-theme-options {"values": {
  "breadcrumb_mobile": "0",
  "breacrumb_prefix": "",
  "breadcrumb_separator": "/",
  "breadcrumbs_font_size": "14px",
  "breadcrumbs_text_color": "var(--awb-color8)",
  "breadcrumb_show_categories": "1",
  "breadcrumb_show_leaf": "1"
}}
```

#### 2.5 Footer

Ask the user:
> "For the **footer** area:
> - Do you want **footer widgets**? (Columns of content like contact info, recent posts, links)
> - How many **columns**? (1-6, default: 4)
> - Do you want a **copyright bar** at the very bottom?
> - What should the **copyright text** say?
> - What **background color** for the footer?
> - Any **special effects**? (Parallax scrolling, sticky footer, etc.)"

```json
mcm/set-theme-options {"values": {
  "footer_widgets": "1",
  "footer_widgets_columns": "4",
  "footer_bg_color": "#1B1B1B",
  "footer_copyright": "1",
  "footer_text": "Copyright 2026 Your Company. All rights reserved.",
  "footer_text_color": "#AAAAAA",
  "footer_link_color": "#CCCCCC",
  "copyright_bg_color": "#111111",
  "copyright_font_size": "13px"
}}
```

#### 2.6 Sidebars

Ask the user:
> "Do you want **sidebars** on any pages? Avada lets you assign sidebars per content type:
>
> - **Pages** — Standard WordPress pages
> - **Blog posts** — Individual blog post pages
> - **Blog archive** — Blog listing pages
> - **Portfolio** — Portfolio items (if using portfolio)
> - **Search results** — Search results page
> - **WooCommerce** — Shop and product pages (if using WooCommerce)
>
> For each, you can choose: no sidebar, left sidebar, right sidebar, or dual sidebars. Which pages should have sidebars?"

```json
mcm/set-theme-options {"values": {
  "pages_sidebar": "None",
  "posts_sidebar": "Blog Sidebar",
  "blog_sidebar_position": "right",
  "blog_archive_sidebar": "Blog Sidebar",
  "blog_archive_sidebar_position": "right",
  "sidebar_bg_color": "transparent",
  "sidebar_heading_color": "var(--awb-color8)"
}}
```

#### 2.7 Sliding Bar (Optional)

Ask the user:
> "Do you want a **sliding bar**? This is a hidden panel that visitors can toggle open, usually from the top or side of the page. It's useful for extra content like contact info, widgets, or promotions. It can slide from the **top**, **right**, **bottom**, or **left** side.
>
> Would you like to enable the sliding bar?"

If yes:
```json
mcm/set-theme-options {"values": {
  "slidingbar_widgets": "1",
  "slidingbar_position": "top",
  "slidingbar_widgets_columns": "3",
  "slidingbar_toggle_style": "triangle",
  "slidingbar_bg_color": "#333333",
  "slidingbar_text_color": "#CCCCCC"
}}
```

---

### Phase 3: CONTENT (Ask before proceeding)

> "Now let's configure how your **content** is displayed — blog posts, portfolio projects, search results, and social sharing."

#### 3.1 Blog

Ask the user:
> "For the **blog**:
> - What **layout** do you prefer?
>   - **Large** — Full-width posts with large featured images
>   - **Medium** — Image on the left, excerpt on the right
>   - **Grid** — Posts in a grid/card layout
>   - **Masonry** — Pinterest-style grid with varying heights
>   - **Timeline** — Posts arranged on a timeline
>   - **Large/Medium Alternate** — Alternating between large and medium layouts
> - How many **columns** for grid layout? (Default: 3)
> - **Pagination style**: Standard numbered pages, infinite scroll, or a 'Load More' button?
> - What post **meta** to show? (Author, date, categories, comments count, tags, read more link)
> - Show a **social sharing box** on each post?
> - Show **related posts** at the bottom of each post?
> - Show the **author info** box?"

```json
mcm/set-theme-options {"values": {
  "blog_layout": "grid",
  "blog_archive_layout": "grid",
  "blog_archive_grid_columns": "3",
  "blog_pagination_type": "pagination",
  "content_length": "excerpt",
  "excerpt_length_blog": "20",
  "featured_images": "1",
  "social_sharing_box": "1",
  "author_info": "1",
  "related_posts": "1",
  "blog_comments": "1",
  "post_meta": "1",
  "post_meta_author": "1",
  "post_meta_date": "1",
  "post_meta_cats": "1",
  "post_meta_comments": "1",
  "post_meta_tags": "0"
}}
```

#### 3.2 Portfolio (if portfolio post type is enabled)

Ask the user:
> "For the **portfolio**:
> - What **archive layout**? (1-6 columns)
> - **Text display**: Show title on rollover, title below image, or no text?
> - Show **pagination**, infinite scroll, or load more?
> - For **single portfolio items**: Show project details, author info, social sharing, related projects, comments?
> - What should the **URL slug** be? (Default: 'portfolio-items')"

```json
mcm/set-theme-options {"values": {
  "portfolio_archive_layout": "portfolio-three",
  "portfolio_archive_columns": "3",
  "portfolio_archive_items": "12",
  "portfolio_archive_pagination_type": "pagination",
  "portfolio_archive_title_display": "all",
  "portfolio_pn_nav": "1",
  "portfolio_social_sharing_box": "1",
  "portfolio_related_posts": "1",
  "portfolio_slug": "portfolio-items"
}}
```

#### 3.3 Search

Ask the user:
> "For the **search** functionality:
> - Should search results include **all content types** or specific ones only?
> - Enable **live search** (results appear as you type)?
> - What **layout** for the search results page? (Large, Medium, Grid, Masonry, Timeline)
> - How many **results per page**?"

```json
mcm/set-theme-options {"values": {
  "search_layout": "grid",
  "search_results_per_page": "12",
  "search_grid_columns": "3",
  "live_search": "1",
  "live_search_min_char_count": "3",
  "search_featured_images": "1"
}}
```

#### 3.4 Social Media

Ask the user:
> "Do you have **social media profiles** to display? Avada can show social icons in the header, footer, and on individual posts. Which networks do you use? (Facebook, Twitter/X, Instagram, LinkedIn, YouTube, Pinterest, TikTok, etc.)
>
> For each network, I'll need the URL to your profile page."

Social icons use a repeater field:
```json
mcm/set-theme-options {"values": {
  "social_media_icons": [
    {"icon": "facebook", "url": "https://facebook.com/yourpage"},
    {"icon": "twitter", "url": "https://twitter.com/yourhandle"},
    {"icon": "instagram", "url": "https://instagram.com/yourhandle"},
    {"icon": "linkedin", "url": "https://linkedin.com/in/yourprofile"}
  ],
  "icons_footer": "1",
  "header_social_links_font_size": "16px",
  "footer_social_links_font_size": "16px"
}}
```

Social sharing box on posts:
```json
mcm/set-theme-options {"values": {
  "sharing_social_tagline": "Share This Story, Choose Your Platform!",
  "social_bg_color": "#F5F5F5"
}}
```

---

### Phase 4: INTEGRATIONS (Conditional — ask only if plugins are active)

#### 4.1 WooCommerce (if WooCommerce is active)

Ask the user:
> "I see **WooCommerce** is active. Let me configure the shop:
> - How many **products per page**? (Default: 12)
> - How many **columns** on the shop page? (Default: 4)
> - **Product image layout**: Avada's custom layout or WooCommerce default?
> - Enable **image zoom** on hover?
> - Enable **quick view** popup on products?
> - Show **variation swatches** on the shop page?
> - Show a **cart icon** in the navigation menu?"

```json
mcm/set-theme-options {"values": {
  "woo_items": "12",
  "woocommerce_shop_page_columns": "4",
  "woocommerce_related_columns": "4",
  "woocommerce_product_images_layout": "avada",
  "woocommerce_product_images_zoom": "1",
  "woocommerce_enable_quick_view": "0",
  "woocommerce_variations": "1",
  "woocommerce_cart_link_main_nav": "1",
  "woocommerce_cart_counter": "1"
}}
```

#### 4.2 Events Calendar (if The Events Calendar is active)

Ask the user:
> "I see **The Events Calendar** is active. Would you like to customize the events styling?
> - **Filter bar** colors (background and text)
> - **Calendar** colors (heading, day cells, borders)
> - **Single event** layout (meta data in sidebar or below content?)
> - Show **social sharing** on events?"

```json
mcm/set-theme-options {"values": {
  "ec_bar_bg_color": "var(--awb-color2)",
  "ec_bar_text_color": "var(--awb-color8)",
  "ec_border_color": "var(--awb-color3)",
  "ec_tooltip_bg_color": "var(--awb-color1)",
  "ec_meta_layout": "sidebar",
  "events_social_sharing_box": "1"
}}
```

#### 4.3 bbPress (if bbPress is active)

Ask the user:
> "I see **bbPress** is active. Would you like to customize the forum styling?
> - **Base font size** for forum text (Default: 12px)
> - **Header background** and **font color** for forum section headers
> - **Border color** for forum borders"

```json
mcm/set-theme-options {"values": {
  "bbp_forum_base_font_size": "14px",
  "bbp_forum_header_bg": "#ebeaea",
  "bbp_forum_header_font_color": "#747474",
  "bbp_forum_border_color": "#ebeaea"
}}
```

---

### Phase 5: ADVANCED (Ask before proceeding)

> "Everything is looking great. Do you want to **fine-tune** any advanced settings? These include performance optimization, lightbox, forms, maintenance mode, privacy/cookie consent, scroll-to-top button, image rollover effects, custom CSS, and more."

#### 5.1 Lightbox

> "The **lightbox** is the popup that appears when clicking on images. Options:
> - **Skin**: Light, dark, metro-white (clean), metro-black, mac, parade, or smooth
> - **Thumbnails**: Show a strip of thumbnails below the lightbox (vertical or horizontal)
> - **Navigation**: Show arrows, enable looping
> - **Autoplay**: Auto-advance through galleries
> - **Social**: Show share buttons in the lightbox"

```json
mcm/set-theme-options {"values": {
  "status_lightbox": "1",
  "lightbox_skin": "metro-white",
  "lightbox_path": "horizontal",
  "lightbox_arrows": "1",
  "lightbox_gallery": "1",
  "lightbox_social": "1",
  "lightbox_title": "1"
}}
```

#### 5.2 Forms Styling

> "For **form inputs** across the site:
> - **Input height**: Height of text inputs (Default: 33px)
> - **Border**: Width, color, radius
> - **Focus color**: Border color when clicking into a field
> - **Background/text colors**
>
> Do you also use **reCAPTCHA** or **Cloudflare Turnstile** for spam protection? I'll need your API keys."

```json
mcm/set-theme-options {"values": {
  "form_input_height": "40px",
  "form_text_size": "14px",
  "form_border_width": "1",
  "form_border_color": "var(--awb-color3)",
  "form_focus_border_color": "var(--awb-color4)",
  "form_border_radius": "4"
}}
```

#### 5.3 Performance

> "**Performance settings** can significantly affect page load speed:
> - **Lazy loading**: Load images/iframes only when they scroll into view (Avada method, WordPress native, or off)
> - **Font loading**: Block (clean render, slower) or Swap (faster, may flash)
> - **Disable emojis script**: If you don't use emojis, saves a request
> - **CSS compiling**: File (recommended), database, or disabled
> - **JS compiler**: Combine JavaScript files (recommended: on)
> - **Image format**: Convert uploads to WebP or AVIF for smaller files
> - **JPEG quality**: 1-100 (default: 82)
>
> Would you like to optimize these settings?"

```json
mcm/set-theme-options {"values": {
  "lazy_load": "avada",
  "lazy_load_iframes": "avada",
  "font_face_display": "swap",
  "emojis_disabled": "disabled",
  "css_cache_method": "file",
  "js_compiler": "1",
  "upload_image_format": "webp",
  "pw_jpeg_quality": "82"
}}
```

#### 5.4 Privacy / Cookie Consent

> "Do you need a **privacy/cookie consent** bar? This is important for GDPR compliance. Options:
> - **Google Fonts mode**: 'Local' downloads fonts to your server (GDPR-friendly) or 'CDN' uses Google's servers
> - **Privacy bar**: A bar at the bottom asking visitors for cookie/embed consent
> - Bar text, button text, colors, and styling"

```json
mcm/set-theme-options {"values": {
  "gfonts_load_method": "local",
  "privacy_embeds": "1",
  "privacy_expiry": "30",
  "privacy_bar": "1",
  "privacy_bar_text": "This website uses cookies and third party services.",
  "privacy_bar_button_text": "Accept",
  "privacy_bar_bg_color": "var(--awb-color8)",
  "privacy_bar_color": "var(--awb-color1)"
}}
```

#### 5.5 Maintenance Mode

> "Do you want to enable **maintenance mode**? This shows a maintenance page or coming-soon page to all visitors except admins.
> - **Maintenance** mode returns a 503 status (site is down for maintenance)
> - **Coming Soon** mode returns a 200 status (site is launching soon)
> - You can select any published page as the template"

```json
mcm/set-theme-options {"values": {
  "maintenance_mode": "maintenance",
  "maintenance_template": "<page_id>",
  "maintenance_page_title": "Under Maintenance",
  "maintenance_robots_meta": "noindex"
}}
```

#### 5.6 Extra Settings

> "Additional settings you may want to configure:
> - **Scroll to top button**: Show a button to scroll back to the top (position, colors, border radius)
> - **Image rollover**: The hover effect on images in grids (direction, icons, gradient colors)
> - **Related posts**: Layout, number of items, columns, carousel behavior
> - **Pagination**: Sizing, font size, border radius
> - **Custom scrollbar**: Enable a styled scrollbar (colors)
> - **Avatar shape**: Square or round for user avatars"

```json
mcm/set-theme-options {"values": {
  "status_totop": "1",
  "totop_position": "right",
  "totop_background": "var(--awb-color4)",
  "image_rollover": "1",
  "related_posts_layout": "title_on_rollover",
  "number_related_posts": "4",
  "related_posts_columns": "4",
  "custom_scrollbar": "1"
}}
```

#### 5.7 Advanced Features / APIs

> "Advanced theme features:
> - **Font Awesome**: Which subsets to load (brands, regular, solid, light)
> - **YouTube/Vimeo/Google Maps**: Enable or disable these scripts
> - **Open Graph**: Enable/disable Open Graph meta tags for social sharing
> - **Rich snippets**: Enable/disable structured data for title, author, date, FAQ
> - **Post types**: Enable/disable Avada Slider, Elastic Slider, Forms, Off Canvas, Portfolio, FAQs"

```json
mcm/set-theme-options {"values": {
  "status_fontawesome": ["fab", "far", "fas"],
  "status_opengraph": "1",
  "status_fusion_portfolio": "1",
  "status_fusion_faqs": "1"
}}
```

#### 5.8 Code Injection

> "Do you have any **tracking codes** or **custom scripts** to add?
> - **Analytics/Tag Manager** code
> - Code before `</head>`
> - Code after `<body>`
> - Code before `</body>`"

```json
mcm/set-theme-options {"values": {
  "google_analytics": "<tracking_code>",
  "space_head": "",
  "space_body_open": "",
  "space_body": ""
}}
```

#### 5.9 Custom CSS

```json
mcm/set-theme-options {"values": {
  "custom_css": "/* Your custom CSS here */"
}}
```

#### 5.10 Custom Auth Pages

> "Would you like to use **custom login, registration, and password reset pages** instead of the default WordPress ones? You'll need to create pages with Avada Forms first."

```json
mcm/set-theme-options {"values": {
  "auth_pages_login_page": "<page_id>",
  "auth_pages_registration_page": "<page_id>",
  "auth_pages_custom_redirect": "auth_pages"
}}
```

#### 5.11 Slideshows & Elastic Slider

> "Configure the **slideshow** behavior for blog/portfolio featured image slideshows:
> - Autoplay, speed, smooth height
>
> And the **Elastic Slider** (if enabled):
> - Dimensions, animation type (sides or center), autoplay, speed"

```json
mcm/set-theme-options {"values": {
  "slideshow_autoplay": "1",
  "slideshow_speed": "7000",
  "tfes_dimensions": {"width": "100%", "height": "400px"},
  "tfes_animation": "sides",
  "tfes_autoplay": "1"
}}
```

#### 5.12 Contact Template

Only relevant if using the Contact page template:
> "If you're using the **Contact page template**: What email address should the form submissions go to? Do you want a Google Map on the page? If so, I'll need a Google Maps API key."

```json
mcm/set-theme-options {"values": {
  "email_address": "contact@example.com",
  "gmap_api": "<api_key>",
  "gmap_address": "Your Address",
  "map_zoom_level": "14"
}}
```

#### 5.13 Responsive

> "**Responsive settings** control how the site adapts to different screen sizes:
> - **Main breakpoint**: Below this width, the site switches to mobile layout (Default: 1000px)
> - **Side header breakpoint**: When side headers switch to top (Default: 800px)
> - **Content/Sidebar breakpoints**: When sidebars stack below content (Default: 800px)
> - **Mobile zoom**: Allow pinch-to-zoom on mobile? (Default: yes)
> - **Responsive typography**: Automatically scale font sizes on smaller screens? (Sensitivity 0 = off, higher = more scaling)
>
> The defaults work well for most sites. Would you like to adjust any breakpoints?"

```json
mcm/set-theme-options {"values": {
  "responsive": "1",
  "grid_main_break_point": "1000",
  "side_header_break_point": "800",
  "content_break_point": "800",
  "sidebar_break_point": "800",
  "mobile_zoom": "1",
  "typography_sensitivity": "0",
  "typography_factor": "1.5"
}}
```

#### 5.14 Background

> "Would you like to set a **background image** or pattern for the body or content area? This is most visible in **boxed layout** mode where the body background shows on the sides."

```json
mcm/set-theme-options {"values": {
  "bg_image": {"url": ""},
  "bg_full": "0",
  "bg_repeat": "repeat",
  "bg_pattern_option": "0",
  "content_bg_image": {"url": ""},
  "content_bg_full": "0",
  "content_bg_repeat": "repeat"
}}
```

#### 5.15 Page-Level Overrides

> "Avada allows **per-page overrides** for many settings. For example, you can hide the header on a specific landing page, change the page title bar color, or set a different sidebar. These use post meta with the `pyre_` prefix."

```json
mcm/update-content {"id": <page_id>, "meta": {
  "pyre_display_header": "no",
  "pyre_display_footer": "no",
  "pyre_page_title_bar": "hide"
}}
```

---

## Procedure (Quick Reference)

### 0) Verify the active theme
Call `mcm/theme-config-guide` — auto-detects the active theme and confirms it is `Avada` (classic theme).

### 1) Read current configuration
```json
mcm/get-theme-options {}
mcm/get-theme-options {"keys": ["primary_color", "header_layout", "layout"]}
mcm/get-theme-mod {}
```

### 2) Apply changes
Use `mcm/set-theme-options`, `mcm/set-theme-mod`, `mcm/set-option`, and `mcm/update-content` as shown in each phase above.

### 3) Cache clearing
The `mcm/set-theme-options` ability **automatically clears** Avada's dynamic CSS cache after updating. No manual cache clearing is needed.

---

## Important: Avada Color System

Avada 7.x+ uses a **Global Color Palette** (AWB Colors). Individual color options reference palette variables `var(--awb-color1)` through `var(--awb-color8)`:

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

## Important: Avada Typography Format

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

## Important: Avada Logo System

| What | Format | Ability |
|------|--------|---------|
| Main logo | `logo` = `{"url": "..."}` in fusion_options | `mcm/set-theme-options` |
| Retina logo | `logo_retina` = `{"url": "..."}` | `mcm/set-theme-options` |
| Sticky logo | `sticky_header_logo` = `{"url": "..."}` | `mcm/set-theme-options` |
| Mobile logo | `mobile_logo` = `{"url": "..."}` | `mcm/set-theme-options` |
| WP custom_logo | `custom_logo` = attachment ID | `mcm/set-theme-mod` |
| Favicon | `fav_icon` = `{"url": "..."}` | `mcm/set-theme-options` |
| WP site icon | `site_icon` = attachment ID | `mcm/set-option` |

> **Both `logo` in fusion_options AND `custom_logo` theme mod must be set** for maximum compatibility.

---

## Minimum Configuration Checklist

When setting up Avada from scratch, at minimum set ALL of these:

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
- [ ] `logo` — Main logo (`{"url": "..."}`)
- [ ] `primary_color` — Primary accent color
- [ ] `bg_color` — Body background
- [ ] `content_bg_color` — Content area background
- [ ] `header_layout` — Header layout (v1-v7)
- [ ] `header_bg_color` — Header background
- [ ] `body_typography` — Body font (array)
- [ ] `h1_typography` — H1 heading (array)
- [ ] `footer_widgets` — Enable footer widgets (`1`)
- [ ] `footer_widgets_columns` — Footer columns
- [ ] `footer_bg_color` — Footer background
- [ ] `footer_copyright` — Enable copyright (`1`)
- [ ] `footer_text` — Copyright text

**Recommended:**
- [ ] `logo_retina` — Retina logo
- [ ] `mobile_logo` — Mobile logo
- [ ] `fav_icon` — Favicon (`{"url": "..."}`)
- [ ] `layout` — Site layout (`wide` or `boxed`)
- [ ] `site_width` — Site width (e.g., `1200px`)
- [ ] `link_color` / `link_hover_color` — Link colors
- [ ] `nav_height` — Navigation height
- [ ] `page_title_bar` — Page title bar display mode
- [ ] `gfonts_load_method` — `local` for GDPR compliance

---

## Verification Checklist

After configuring, verify each area:

- [ ] Logo displays in the header (desktop, mobile, and sticky)
- [ ] Colors display correctly on the frontend
- [ ] Header layout and styling are correct
- [ ] Page title bar and breadcrumbs display correctly
- [ ] Footer widgets and copyright display correctly
- [ ] Typography (body, headings) renders correctly
- [ ] Blog layout and meta display settings work
- [ ] Portfolio archive/single display correctly (if applicable)
- [ ] Search results page renders correctly
- [ ] Social media icons display in header and footer
- [ ] WooCommerce shop page and products display correctly (if applicable)
- [ ] Sidebars appear on the correct pages
- [ ] Responsive breakpoints trigger correctly
- [ ] Lightbox opens correctly when clicking images
- [ ] Privacy bar appears if enabled
- [ ] Dynamic CSS has been regenerated (automatic)

---

## Failure Modes / Debugging

- **Logo not showing:** Check BOTH `logo` in fusion_options (URL format `{"url": "..."}`) AND `custom_logo` theme mod (attachment ID). Both must be set.
- **Changes not visible:** The MCP ability auto-clears Avada's compiled CSS cache. Clear browser cache if needed.
- **Option not saving:** `mcm/set-theme-options` reads the full array and merges only specified keys — never replaces the entire array.
- **Page-level override not working:** Page meta keys use `pyre_` prefix (e.g., `pyre_header_bg_color`).
- **Multilingual sites:** Option key may be language-suffixed (e.g., `fusion_options_es`).
- **Color variables:** Avada 7.x uses `var(--awb-colorN)` references — set actual hex values or update the global palette.
- **Typography not applying:** Must be an array with ALL properties (font-family, font-size, font-weight, line-height, letter-spacing, font-style, text-transform, color). A simple string like `"16px"` will NOT work.
- **Social icons not showing:** Check that `social_media_icons` is a properly formatted repeater array with `icon` and `url` fields.
- **Sidebar not appearing:** Verify the sidebar name exists (check via `mcm/get-theme-options {"keys": ["pages_sidebar"]}`) and position is set correctly.
- **Breadcrumbs overridden:** If Yoast SEO or RankMath is active, their breadcrumbs override Avada's.
- **Portfolio/FAQ slugs changed:** After changing `portfolio_slug` or `faq_slug`, flush permalinks.

---

## Reference files

- **[theme-options.md](references/theme-options.md)** — Complete list of all 600+ option IDs with types, defaults, descriptions, and valid choices
- **[../global-styles-api.md](../global-styles-api.md)** — Shared reference (see Section 0 for Classic vs FSE differences)
