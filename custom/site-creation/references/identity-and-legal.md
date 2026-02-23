# Phases 6–7: Site Identity & Legal Pages

## Phase 6 — Site Identity

Configure the site identity using MCP abilities:

```json
// Site title and tagline
mcm/set-option {"name": "blogname", "value": "Site Name"}
mcm/set-option {"name": "blogdescription", "value": "Site Tagline"}

// Logo — first upload the image, then set the theme mod
mcm/upload-media {"url": "https://example.com/logo.png", "title": "Site Logo"}
// Use the returned attachment ID:
mcm/set-theme-mod {"key": "custom_logo", "value": <attachment_id>}

// Favicon — upload and set
mcm/upload-media {"url": "https://example.com/favicon.png", "title": "Favicon"}
mcm/set-option {"name": "site_icon", "value": <attachment_id>}

// Static front page (if decided in Phase 2)
mcm/set-option {"name": "show_on_front", "value": "page"}
mcm/set-option {"name": "page_on_front", "value": <homepage_id>}
mcm/set-option {"name": "page_for_posts", "value": <blog_page_id>}
```

If theme colors were not fully configured in Phase 3, do it now. Call `mcm/theme-config-guide` to see the available color options for the active theme, then apply the user's color palette using `mcm/set-global-styles` (block themes) or `mcm/set-theme-options` (classic themes).

---

## Phase 7 — Legal Pages

Create legal pages with base text, always indicating that **they must be reviewed by a legal professional**.

### Preliminary Questions

1. Company name or site owner's name.
2. Tax ID / Business registration number.
3. Physical address of the responsible party.
4. Contact email.
5. Are personal data collected through forms? (contact, registration, purchase)
6. Are third-party cookies used? (Analytics, social media, advertising)
7. Under which legislation does it operate? (GDPR, local data protection laws, etc.)

### Pages to Create

1. **Legal Notice** — Owner, site purpose, intellectual property, limitation of liability.
2. **Privacy Policy** — Data controller, data collected, purposes, legal basis, recipients, user rights, retention period.
3. **Cookie Policy** — What cookies are, types used, purpose, management, link to the banner settings panel.
4. **Terms and Conditions** (especially for e-commerce) — Terms of use, purchase, shipping, returns, warranties.

Always include this visible notice on each legal page: *"This text is for guidance purposes and must be reviewed by a legal professional to ensure regulatory compliance."*

Configure SEO for each legal page. Ask whether they should be set to noindex.
