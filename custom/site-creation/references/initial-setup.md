# Phases 0–2: Maintenance Mode, Initial Questions & Base Configuration

## Phase 0 — Maintenance Mode

Before touching anything, install and activate a maintenance mode plugin (WP Maintenance Mode, Coming Soon Page, or similar) so the site is not visible to the public during construction.

---

## Phase 1 — Initial Questions

Before installing or configuring anything, ask the user:

1. **Site type:** Corporate/institutional, online store, personal blog, portfolio, landing page, magazine/media, community/forum, or other.
2. **Site name.**
3. **Tagline or short description** (if they have one).
4. **Primary language** of the site.
5. **Does it need multiple languages?** If yes, which ones.
6. **Do they have a logo?** Ask them to provide it. If not, a basic one can be created.
7. **Do they have a favicon?** If not, one will be generated from the logo.
8. **Color palette** (corporate colors or preferences).
9. **Timezone** of the business or target audience.
10. **Do they want generated images for page content?** Featured images are always created. Gemini is assumed to be configured for image generation.

The answers absolutely condition everything: plugins, theme, pages, configuration. Do not proceed without them.

---

## Phase 2 — WordPress Base Configuration

### General Settings

Configure based on Phase 1 answers:

- Site title and tagline.
- Site language.
- Timezone.
- Date and time format appropriate for the language/country.
- **Permalinks:** Set to "Post name" (`/%postname%/`) unless the user specifies otherwise.

### Default Content Cleanup

Delete all WordPress sample content:

- "Hello World" post.
- "Sample Page" page.
- Sample comment.
- Pre-installed plugins that won't be used (Hello Dolly, etc.).

### Search Engine Visibility

Enable **"Discourage search engines from indexing this site"** (Settings > Reading) during the entire construction process. The site is not ready yet and must not be indexed. This will be reviewed before launch in Phase 13.

### Reading Settings

Ask whether the homepage should be a static page or display the latest blog posts.

### Comments Settings

Ask whether they want to allow comments. If yes, set up basic moderation. If not, disable them globally.
