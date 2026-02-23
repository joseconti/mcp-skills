# Theme Configuration API Reference

How to read and write theme configuration via MCP Content Manager abilities.

---

## 0. Classic Themes vs Block (FSE) Themes — Key Differences

**CRITICAL:** The storage mechanism is completely different depending on the theme type. You MUST identify the theme type before attempting configuration.

### How to detect the theme type

Call `mcm/theme-config-guide` — it auto-detects and returns the theme type (block or classic), slug, and available configuration options.

### Classic Theme — Where settings are stored

| Setting | Storage | MCP Ability |
|---------|---------|-------------|
| Colors, fonts, layout | `wp_options` → theme-specific key (serialized) | `mcm/get-theme-options` / `mcm/set-theme-options` |
| Navigation menus | `wp_terms` + `wp_posts` (nav_menu_item) | `mcm/get-menus` / `mcm/update-menu` |
| Header/Background image | `wp_options` → `theme_mods_{slug}` | `mcm/get-theme-mod` / `mcm/set-theme-mod` |
| Site identity | `wp_options` → `blogname`, `blogdescription`, `site_icon` | `mcm/set-option` |
| Theme-specific options | `wp_options` → custom keys (e.g., `fusion_options`, `the7mk2`) | `mcm/get-theme-options` / `mcm/set-theme-options` |

**Example: configure a classic theme**

```json
// Read current Avada options
mcm/get-theme-options {}
// → auto-detects fusion_options and returns all values

// Update specific options
mcm/set-theme-options {"values": {"primary_color": "#E94560", "header_layout": "v1"}}

// Set site logo
mcm/set-theme-mod {"key": "custom_logo", "value": 123}
```

### Block Theme (FSE) — Where settings are stored

| Setting | Storage | MCP Ability |
|---------|---------|-------------|
| Colors, fonts, layout, spacing, block styles | `wp_posts` → type `wp_global_styles` (JSON) | `mcm/get-global-styles` / `mcm/set-global-styles` |
| Templates | `wp_posts` → type `wp_template` | `mcm/update-content` |
| Template Parts (header, footer) | `wp_posts` → type `wp_template_part` | `mcm/update-content` |
| Navigation menus | `wp_posts` → type `wp_navigation` (block content) | `mcm/create-fse-navigation` / `mcm/update-fse-navigation` |
| Site identity | `wp_options` → `blogname`, `blogdescription`, `site_icon` | `mcm/set-option` |
| Custom logo | `wp_options` → `theme_mods_{slug}` | `mcm/set-theme-mod` |

**Example: configure a block theme**

```json
// Read current Global Styles
mcm/get-global-styles {"section": "both", "origin": "all"}

// Change background and text colors
mcm/set-global-styles {
  "styles": {
    "color": {
      "background": "var:preset|color|base",
      "text": "var:preset|color|contrast"
    }
  }
}
```

### Summary Decision Tree

```
Is the theme a block theme (FSE)?
├── YES (Block/FSE Theme):
│   ├── Colors/Fonts/Layout → mcm/get-global-styles + mcm/set-global-styles
│   ├── Page layouts → mcm/update-content (post_type=wp_template)
│   ├── Header/Footer → mcm/update-content (post_type=wp_template_part)
│   └── Menus → mcm/create-fse-navigation / mcm/update-fse-navigation
│
└── NO (Classic Theme):
    ├── Colors/Fonts/Layout → mcm/get-theme-options + mcm/set-theme-options
    ├── Page layouts → PHP template files (not DB-configurable)
    ├── Sidebar content → Widgets (use mcm/set-option if needed)
    └── Menus → mcm/get-menus + mcm/update-menu
```

---

## 1. Global Styles (Colors, Typography, Spacing, Layout, Block Styles)

### Reading Global Styles

```json
// Read all settings and styles (merged: core + theme + user)
mcm/get-global-styles {"section": "both", "origin": "all"}

// Read only user customizations (overrides)
mcm/get-global-styles {"section": "both", "origin": "user"}

// Read only settings (presets: palette, fonts, sizes)
mcm/get-global-styles {"section": "settings"}

// Read only styles (applied CSS values)
mcm/get-global-styles {"section": "styles"}

// Drill into a specific path
mcm/get-global-styles {"section": "settings", "path": "color.palette"}

// Read block-level styles
mcm/get-global-styles {"section": "styles", "block_name": "core/button"}
```

### Updating Global Styles

```json
// Update with deep merge (default — only changes specified keys)
mcm/set-global-styles {
  "settings": {
    "color": {
      "palette": {
        "theme": [
          {"color": "#FFFFFF", "name": "Base", "slug": "base"},
          {"color": "#1A1A2E", "name": "Contrast", "slug": "contrast"},
          {"color": "#E94560", "name": "Accent 1", "slug": "accent-1"}
        ]
      }
    }
  }
}

// Replace entire section (caution!)
mcm/set-global-styles {
  "styles": {"color": {"background": "#fff", "text": "#000"}},
  "merge_mode": "replace"
}
```

### Resetting Global Styles

```json
// Reset everything to theme defaults (requires confirmation)
mcm/reset-global-styles {"confirm": true}

// Reset only settings
mcm/reset-global-styles {"section": "settings", "confirm": true}

// Reset only styles
mcm/reset-global-styles {"section": "styles", "confirm": true}
```

**Important:** Always read current Global Styles before updating — use deep merge (default) to avoid wiping other settings.

---

## 2. Site Options (Blog Name, Tagline, Homepage, etc.)

```json
// Read site options
mcm/get-option {"name": "blogname"}
mcm/get-option {"name": "show_on_front"}

// Set site options
mcm/set-option {"name": "blogname", "value": "My Site"}
mcm/set-option {"name": "blogdescription", "value": "My tagline"}
mcm/set-option {"name": "show_on_front", "value": "page"}
mcm/set-option {"name": "page_on_front", "value": 10}
mcm/set-option {"name": "page_for_posts", "value": 20}
mcm/set-option {"name": "site_icon", "value": 123}
```

### Key Options

| Option Key | Description | Values |
|-----------|-------------|--------|
| `blogname` | Site title | String |
| `blogdescription` | Site tagline | String |
| `site_icon` | Favicon attachment ID | Integer |
| `show_on_front` | Homepage display | `posts` or `page` |
| `page_on_front` | Static front page ID | Integer |
| `page_for_posts` | Posts page ID | Integer |
| `posts_per_page` | Posts per page | Integer |
| `date_format` | Date format string | PHP date format |
| `time_format` | Time format string | PHP time format |
| `timezone_string` | Timezone | e.g. `Europe/Madrid` |

---

## 3. Theme Mods (Logo, Custom Background, etc.)

```json
// Read all theme mods
mcm/get-theme-mod {}

// Read a specific theme mod
mcm/get-theme-mod {"key": "custom_logo"}

// Set the site logo (requires attachment ID from mcm/upload-media)
mcm/set-theme-mod {"key": "custom_logo", "value": 123}

// Set header image
mcm/set-theme-mod {"key": "header_image", "value": "https://example.com/header.jpg"}

// Remove a theme mod
mcm/set-theme-mod {"key": "custom_logo", "action": "remove"}
```

---

## 4. Templates & Template Parts

Templates and template parts can be managed with `mcm/search-content` and `mcm/update-content`:

```json
// List templates
mcm/search-content {"post_type": "wp_template", "per_page": 50}

// List template parts
mcm/search-content {"post_type": "wp_template_part", "per_page": 50}

// Update a template part (e.g., replace header content)
mcm/update-content {"id": <template_part_id>, "content": "<!-- wp:group -->...<!-- /wp:group -->"}
```

---

## 5. Navigation Menus

### Block themes (FSE)

```json
// List FSE navigations
mcm/list-fse-navigations {}

// Create a new FSE navigation
mcm/create-fse-navigation {
  "title": "Main Navigation",
  "links": [
    {"label": "Home", "url": "/"},
    {"label": "Blog", "url": "/blog"}
  ]
}

// Update an existing FSE navigation
mcm/update-fse-navigation {
  "id": <navigation_id>,
  "links": [
    {"label": "Home", "url": "/"},
    {"label": "About", "url": "/about"},
    {"label": "Blog", "url": "/blog"}
  ]
}
```

### Classic themes

```json
// List menus
mcm/get-menus {}

// Update a menu
mcm/update-menu {
  "id": <menu_id>,
  "items": [
    {"title": "Home", "url": "/"},
    {"title": "About", "url": "/about"}
  ]
}
```

---

## 6. Changing Colors Example (Full Flow)

To change the color palette of a block theme:

```json
// 1. Read current Global Styles
mcm/get-global-styles {"section": "settings", "path": "color.palette"}

// 2. Update with new palette
mcm/set-global-styles {
  "settings": {
    "color": {
      "palette": {
        "theme": [
          {"color": "#FFFFFF", "name": "Base", "slug": "base"},
          {"color": "#1A1A2E", "name": "Contrast", "slug": "contrast"},
          {"color": "#E94560", "name": "Accent 1", "slug": "accent-1"}
        ]
      }
    }
  }
}
// Cache is automatically cleared by the MCP ability
```

---

## 7. Changing Typography Example (Full Flow)

```json
// 1. Read current typography
mcm/get-global-styles {"section": "styles", "path": "typography"}

// 2. Update typography
mcm/set-global-styles {
  "styles": {
    "typography": {
      "fontFamily": "var:preset|font-family|heading",
      "fontSize": "var:preset|font-size|medium",
      "fontWeight": "400",
      "lineHeight": "1.6"
    }
  }
}
```

---

## Important Notes

- Always read current Global Styles before updating — use deep merge (default) to avoid wiping other settings
- Cache is automatically cleared by the MCP abilities after updates
- Global Styles user customizations override theme.json defaults
- Use `var:preset|{type}|{slug}` format to reference preset colors/fonts/sizes in styles
- Template and template-part changes create custom versions that override theme files
- ALWAYS ask the user what they want to change before applying any configuration
