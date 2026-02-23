---
name: wordpress-theme-customizer
description: >
  Customize and configure any WordPress theme. Use this skill when the user wants to change the
  design of their site, modify colors, typography, header, footer, layout, or any visual aspect
  of the active theme. Also when they ask to "change the design", "customize the theme", "modify
  the appearance", "configure the theme", "change colors", "change fonts", "adjust the header/footer",
  or any request related to the visual appearance and configuration of the WordPress site. Searches
  first for a theme-specific skill before performing scans. Compatible with both classic themes and
  block (FSE) themes.
---

# WordPress Theme Customizer

## Purpose

Customize and configure any WordPress theme — classic or block (FSE). This skill acts as an orchestrator: it finds the best way to discover and apply configuration for the active theme.

---

## Decision Flow

Follow these steps **in strict order** when the user asks to customize, configure, or modify the design of their WordPress theme.

### Step 1 — Detect the active theme and its type

Call `mcm/theme-config-guide` first. This returns:

- Theme name and slug
- Theme type: **block (FSE)** or **classic**
- Available configuration options and MCP abilities to use

**CRITICAL:** The theme type determines which abilities to use. See [../INDEX.md](../INDEX.md) and [../global-styles-api.md](../global-styles-api.md) Section 0 for the full Classic vs FSE comparison.

| Theme Type | Settings Storage | Read Ability | Write Ability |
|---|---|---|---|
| Block (FSE) | `wp_global_styles` post (JSON) | `mcm/get-global-styles` | `mcm/set-global-styles` |
| Classic | `wp_options` (serialized array) | `mcm/get-theme-options` | `mcm/set-theme-options` |
| Both | `theme_mods_{slug}` | `mcm/get-theme-mod` | `mcm/set-theme-mod` |
| Both | `wp_options` (site identity) | `mcm/get-option` | `mcm/set-option` |

### Step 2 — Check for a theme-specific skill

Check if a dedicated configuration skill exists for the active theme. Theme skills follow the naming convention `theme-{slug}-config` and are located in the `themes/` directory:

| Theme | Skill Directory | Type |
|---|---|---|
| Avada | [../avada/](../avada/) | Classic |
| The7 | [../dt-the7/](../dt-the7/) | Classic |
| Twenty Twenty-Five | [../twentytwentyfive/](../twentytwentyfive/) | Block (FSE) |
| Twenty Twenty-Four | [../twentytwentyfour/](../twentytwentyfour/) | Block (FSE) |
| Twenty Twenty-Three | [../twentytwentythree/](../twentytwentythree/) | Block (FSE) |

**If a specific skill exists:** Use it. It is the most reliable source because it was created specifically for that theme with all its options documented. Inform the user:

> "A specific configuration skill exists for your theme. I will use it to configure it."

Do NOT offer the other options. Follow the theme-specific skill's procedure directly.

**If no specific skill exists:** Go to Step 3.

### Step 3 — Offer scan options to the user

Inform the user that no specific skill exists for their theme and present two options. **Let the user choose — do not decide for them.**

---

**Option A — Standard scan (fast, may not be complete)**

> "I can analyze your theme by reading its configuration through standard WordPress APIs (Global Styles, Customizer settings, theme options, theme mods, etc.). This is fast and uses normal resources, but if your theme has custom option panels that don't use the standard WordPress API, it may not detect all options."

---

**Option B — Full source code scan (reliable, higher cost)**

> "I can scan the theme's entire source code to discover absolutely all configuration options, including custom panels, proprietary frameworks, and any non-standard settings. This method is the most reliable but reads many files and may have a high token cost if you're using the Anthropic API. Do you want to continue?"

Only proceed with Option B after the user explicitly confirms.

---

## Option A — Standard Scan

### How it works

The standard scan uses existing MCP abilities to discover configuration without reading source files.

#### For block themes (FSE)

1. **Global Styles** — Read all settings and styles:
   ```json
   mcm/get-global-styles {"section": "both", "origin": "all"}
   ```
   This returns: color palette, typography (font families, sizes), spacing presets, layout settings (content/wide widths), and all per-block style overrides.

2. **User customizations** — Read only what the user has changed:
   ```json
   mcm/get-global-styles {"section": "both", "origin": "user"}
   ```

3. **Templates and template parts** — Discover the site structure:
   ```json
   mcm/search-content {"post_type": "wp_template", "per_page": 50}
   mcm/search-content {"post_type": "wp_template_part", "per_page": 50}
   ```

4. **FSE Navigation** — Available menus:
   ```json
   mcm/list-fse-navigations {}
   ```

5. **Theme mods** — Logo, header image, etc.:
   ```json
   mcm/get-theme-mod {}
   ```

6. **Site identity** — Title, tagline, homepage:
   ```json
   mcm/get-option {"name": "blogname"}
   mcm/get-option {"name": "blogdescription"}
   mcm/get-option {"name": "show_on_front"}
   ```

#### For classic themes

1. **Theme options** — Read all stored options:
   ```json
   mcm/get-theme-options {}
   ```
   This auto-detects the option key (e.g., `fusion_options` for Avada, `the7mk2` for The7) and returns all values.

2. **Theme mods** — Logo, header image, background, etc.:
   ```json
   mcm/get-theme-mod {}
   ```

3. **Menus** — Navigation menu locations and items:
   ```json
   mcm/get-menus {}
   ```

4. **Site identity** — Title, tagline, homepage:
   ```json
   mcm/get-option {"name": "blogname"}
   mcm/get-option {"name": "blogdescription"}
   mcm/get-option {"name": "show_on_front"}
   ```

### Report format

Generate a structured report with all discovered options, grouped by category:

- **Site Identity** — Logo, favicon, site title, tagline
- **Colors** — Palette, backgrounds, text, links, buttons
- **Typography** — Font families, sizes, weights, line heights
- **Header** — Layout, options, transparency, sticky
- **Footer** — Layout, columns, widgets, credits
- **Layout** — Content width, wide width, sidebars, containers
- **Navigation** — Menu locations, menu styles
- **Blog / Posts** — Archive layout, single post layout
- **Pages** — Layout, sidebar, per-page options
- **WooCommerce** — Shop layout, product display (if applicable)
- **Advanced** — Custom CSS, code in header/footer

For each option include:
- Setting name
- Where to configure it (admin path or MCP ability)
- Possible values or control type
- Current value

### Limitations

Inform the user that this scan may NOT detect:
- Custom option panels built with proprietary frameworks (Redux, Carbon Fields, CMB2, Jeune, etc.)
- Options stored in custom database tables
- Configurations implemented in pure JavaScript without PHP hooks
- Integrated page builders with their own settings systems

---

## Option B — Full Source Code Scan

### Pre-scan check: determine the scan method

Before scanning, detect which method is available:

```json
// Check if WP-CLI is available (preferred method)
mcm/check-wpcli {}
```

- **If WP-CLI is available:** Use WP-CLI commands via `mcm/execute-wpcli` — faster and more structured.
- **If WP-CLI is NOT available:** Fall back to `mcm/list-files` and `mcm/read-file` MCP abilities.

### Confirmation before proceeding

> "I'm going to analyze all PHP, JSON, and JS files of the theme. This involves reading a significant number of files. If you're using the Anthropic API, this process may consume a notable amount of tokens and therefore have a significant cost. Do you want to continue?"

Only proceed if the user confirms.

### Pass 1 — Structure map (fast)

#### With WP-CLI

```json
// Get theme path
mcm/execute-wpcli {"command": "theme path --theme=<active-theme-slug>"}

// List theme files
mcm/execute-wpcli {"command": "eval 'echo json_encode(glob(get_template_directory() . \"/**/*.php\", GLOB_BRACE));'"}

// Search for key patterns in theme PHP files
mcm/execute-wpcli {"command": "eval '$dir = get_template_directory(); echo shell_exec(\"grep -rl \\\"customize_register\\\" \" . escapeshellarg($dir));'"}
```

#### Without WP-CLI (fallback)

```json
// List theme directory structure
mcm/list-files {"path": "wp-content/themes/<active-theme-slug>/", "recursive": true}

// Read key files
mcm/read-file {"path": "wp-content/themes/<active-theme-slug>/functions.php"}
mcm/read-file {"path": "wp-content/themes/<active-theme-slug>/theme.json"}
mcm/read-file {"path": "wp-content/themes/<active-theme-slug>/style.css"}
```

#### What to identify in Pass 1

Search for these patterns across all theme PHP files:

| Pattern | Indicates |
|---|---|
| `customize_register` | Customizer sections/settings/controls |
| `add_menu_page`, `add_submenu_page`, `add_theme_page` | Admin option pages |
| `register_setting`, `add_settings_section` | WordPress Settings API |
| `Redux`, `ReduxFramework`, `CSF`, `Carbon_Fields`, `CMB2` | Third-party option frameworks |
| `add_theme_support` | Theme support declarations |
| `register_nav_menus` | Navigation menu locations |
| `register_sidebar` | Widget areas |
| `register_block_pattern` | Block patterns |
| `wp_enqueue_script.*admin` | Admin scripts (possible JS panels) |
| `add_meta_box` | Custom meta boxes (per-page options) |
| `rest_api_init` | Custom REST endpoints |
| `wp_ajax_` | Custom AJAX actions |

With the results, identify which files are relevant and which are not.

### Pass 2 — Deep read (relevant files only)

Read only the files identified in Pass 1. For each file:

1. **Customizer files:** Extract all panels, sections, settings, and controls. Document control type, default values, available options.

2. **Custom option panels:** Identify the framework used. Extract the options structure: fields, types, defaults, dependencies.

3. **Admin pages:** Document which options they expose and how they are saved (`option`, `theme_mod`, custom table).

4. **theme.json** (block themes): Extract the complete design configuration: color palette, typography, spacing, layout, per-block styles, custom properties.

5. **Templates and parts** (FSE themes): Document the site structure, which parts are editable, and which template is used for each content type.

6. **Admin JavaScript:** If panels are built in JS/React, identify what options they expose.

7. **CSS main files:** Identify CSS custom properties (variables) that can be modified.

### Report format

Generate a complete structured report with:

1. **Theme summary:** Name, version, author, type (classic, FSE, hybrid), frameworks used.

2. **Complete options map**, grouped by:
   - Identity (logo, favicon, site name)
   - Colors (palette, backgrounds, text, links, buttons)
   - Typography (fonts, sizes, weights)
   - Header (layout, options, transparency, sticky)
   - Footer (layout, columns, widgets, credits)
   - General layout (content width, sidebars, containers)
   - Navigation (menu locations, menu styles, mobile menu)
   - Blog / Posts (archive layout, single post layout)
   - Pages (layout, sidebar, per-page options)
   - WooCommerce (if applicable: shop layout, product, cart)
   - Advanced options (custom CSS, code in header/footer)

3. **For each option:**
   - Human-readable name
   - Where to configure (exact admin path: Customize > X > Y, or Panel > Tab > Section)
   - Control type (color picker, select, toggle, slider, textarea, etc.)
   - Possible values or range
   - Default value
   - How it is stored internally (`theme_mod`, `option`, etc.)

4. **Dependencies between options** (if changing one activates or deactivates others).

5. **Options not available in the admin** but modifiable via code (filters, hooks, constants).

After generating the report, ask the user what they want to configure or modify.

---

## Executing Changes

Once the user indicates what they want to change (whether using a theme-specific skill, Option A, or Option B), follow this procedure:

### 1) Confirm the change

> "I'm going to change [X] from [current value] to [new value]. Is that correct?"

### 2) Execute the change via the appropriate method

#### Block themes (FSE)

| Change Type | MCP Ability | Example |
|---|---|---|
| Colors, fonts, layout, spacing | `mcm/set-global-styles` | `{"styles": {"color": {"background": "#fff"}}}` |
| Color palette presets | `mcm/set-global-styles` | `{"settings": {"color": {"palette": {"theme": [...]}}}}` |
| Templates | `mcm/update-content` | Update `wp_template` post |
| Template parts (header/footer) | `mcm/update-content` | Update `wp_template_part` post |
| Navigation menus | `mcm/create-fse-navigation` / `mcm/update-fse-navigation` | Block-based navigation |
| Reset to defaults | `mcm/reset-global-styles` | `{"confirm": true}` |

See [../global-styles-api.md](../global-styles-api.md) for the full API reference.

#### Classic themes

| Change Type | MCP Ability | Example |
|---|---|---|
| Theme options (colors, layout, etc.) | `mcm/set-theme-options` | `{"values": {"primary_color": "#E94560"}}` |
| Theme mods (logo, background) | `mcm/set-theme-mod` | `{"key": "custom_logo", "value": 123}` |
| Navigation menus | `mcm/update-menu` | Update menu items |
| Per-page options (post meta) | `mcm/update-content` | `{"id": 42, "meta": {"pyre_header_bg_color": "#FFF"}}` |

#### Both theme types

| Change Type | MCP Ability | Example |
|---|---|---|
| Site title | `mcm/set-option` | `{"name": "blogname", "value": "My Site"}` |
| Tagline | `mcm/set-option` | `{"name": "blogdescription", "value": "My tagline"}` |
| Favicon | `mcm/set-option` | `{"name": "site_icon", "value": 123}` |
| Logo | `mcm/set-theme-mod` | `{"key": "custom_logo", "value": 123}` |
| Homepage display | `mcm/set-option` | `{"name": "show_on_front", "value": "page"}` |
| Static front page | `mcm/set-option` | `{"name": "page_on_front", "value": 10}` |
| Posts page | `mcm/set-option` | `{"name": "page_for_posts", "value": 20}` |

### 3) Verify the result

Confirm the change was applied by reading back the value:

- Block themes: `mcm/get-global-styles {"section": "both", "origin": "user"}`
- Classic themes: `mcm/get-theme-options {"keys": ["changed_option_id"]}`
- Theme mods: `mcm/get-theme-mod {"key": "changed_key"}`
- Options: `mcm/get-option {"name": "changed_option"}`

### 4) Child theme warning

If the user is modifying theme files directly (not via database-stored options), warn them:

> "These changes are applied directly to the theme files. They will be lost when the theme is updated. I recommend creating a child theme if you don't have one."

---

## Generating a Theme-Specific Skill (optional)

After completing a scan (especially the full source scan), offer the user:

> "I've discovered all the configuration options for your theme. Would you like me to generate a specific skill for this theme? That way, next time you or anyone else wants to configure this theme, the assistant will have all the information without needing to scan again."

If they accept, generate a skill following the structure in [../INDEX.md](../INDEX.md):

```
themes/{theme-slug}/
├── SKILL.md              # Main configuration guide
└── references/
    └── theme-options.md  # Complete list of option IDs, types, and defaults
```

The SKILL.md should follow the same format as existing theme skills (see [../avada/SKILL.md](../avada/SKILL.md) or [../twentytwentyfive/SKILL.md](../twentytwentyfive/SKILL.md) as models).

After generating the skill, update [../INDEX.md](../INDEX.md) to include the new theme.

---

## Reference Files

- **[../INDEX.md](../INDEX.md)** — Index of all theme-specific skills
- **[../global-styles-api.md](../global-styles-api.md)** — Shared API reference for reading and writing theme configuration
- **[../../site-creation/SKILL.md](../../site-creation/SKILL.md)** — Site creation skill (Phase 3 handles initial theme configuration)
