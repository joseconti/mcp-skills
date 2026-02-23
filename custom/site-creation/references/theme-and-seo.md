# Phases 3–4: Theme Selection & SEO Plugin

## Phase 3 — Theme Selection

### Questions

1. **Do they have a specific theme in mind?** If yes, install it.
2. If not, offer alternatives based on the site type:
   - **Corporate/institutional:** Astra, GeneratePress, Kadence
   - **Online store:** Storefront (official WooCommerce), Astra, Flatsome, OceanWP
   - **Personal blog:** GeneratePress, Kadence, Twenty Twenty-Five, Astra
   - **Portfolio:** Astra, Kadence, GeneratePress

3. Install and activate the chosen theme:

```json
// Install from WordPress.org
mcm/install-theme {"slug": "twentytwentyfive"}

// Or install from a ZIP URL (premium themes)
mcm/install-theme {"url": "https://example.com/theme.zip"}
```

### Theme Configuration

After installing the theme, configure its visual appearance based on the user's preferences (colors, typography, layout). Follow this workflow:

#### Step 1: Get the theme configuration guide

```json
mcm/theme-config-guide {}
```

This auto-detects the active theme and returns the specific configuration guide with all available options, slugs, defaults, and examples. **Always call this first** — it tells you exactly what can be configured and how.

#### Step 2: Read current theme configuration

For **block themes** (Twenty Twenty-Five, Twenty Twenty-Four, Kadence, etc.):

```json
mcm/get-global-styles {"section": "both", "origin": "all"}
```

For **classic themes** (Avada, The7, Astra classic, etc.):

```json
mcm/get-theme-options {}
```

#### Step 3: Apply the user's color palette

Ask the user for their brand colors, then apply them:

For **block themes**:

```json
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
```

For **classic themes**:

```json
mcm/set-theme-options {
  "values": {
    "primary_color": "#E94560",
    "header_bg_color": "#FFFFFF"
  }
}
```

#### Step 4: Configure typography (if requested)

For **block themes**:

```json
mcm/set-global-styles {
  "styles": {
    "typography": {
      "fontFamily": "var:preset|font-family|manrope",
      "fontSize": "var:preset|font-size|medium"
    }
  }
}
```

#### Step 5: Configure layout widths (if needed)

For **block themes**:

```json
mcm/set-global-styles {
  "settings": {
    "layout": {
      "contentSize": "720px",
      "wideSize": "1200px"
    }
  }
}
```

**Important:** Deep merge is the default — changing one setting does NOT wipe others. Only the specified keys are updated.

#### Advanced theme configuration

For in-depth theme customization beyond the initial setup (custom option panels, full source code scans, per-block styles, etc.), use the **`wordpress-theme-customizer`** skill which handles the complete theme configuration workflow for both classic and block (FSE) themes.

---

## Phase 4 — SEO Plugin

SEO is installed **before creating any content** because every page, post, or product created must have complete SEO from the start. If you create content first, you'll have to go back and review everything later.

### Process

1. Offer alternatives: Yoast SEO, Rank Math, SEOPress, All in One SEO (AIOSEO).
2. Ask which they prefer. You can guide them: "Rank Math is very comprehensive and popular, Yoast is the classic choice."
3. Install, activate, and run the basic configuration:

```json
mcm/install-plugin {"slug": "wordpress-seo"}
```

4. Configure via the plugin's options:
   - Initial setup wizard
   - Site title and separator
   - Content types to index
   - Social metadata (Open Graph)
   - XML Sitemap
   - Robots.txt

5. **Permanent rule:** From this point on, every page/post/product you create must have:
   - Optimized SEO title
   - Meta description
   - Clean, optimized slug
   - Alt text on all images
