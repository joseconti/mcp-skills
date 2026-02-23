# Phases 11–13: Images/Media, Final Configurations & Launch

## Phase 11 — Images and Media

Rules that apply throughout the entire process:

- **Featured image:** mandatory on all pages, posts, and products. No exceptions.
- **Content images:** only if the user authorized them in Phase 1.
- **Generation:** Gemini is used (assumed configured).
- **Alt text:** mandatory on all images, optimized for SEO.
- **Optimization:** ask if they want to install an image optimization plugin (Smush, ShortPixel, Imagify).

---

## Phase 12 — Final Configurations

### 404 Page

Create a user-friendly 404 page with: clear message, search box, links to main pages.

### Widgets and Sidebar

Ask if they want widgets in the sidebar and/or footer. Configure based on the site type (search, categories, recent posts, social media...).

### Footer

Configure footer areas with: contact information, legal menu, social media links (if applicable), copyright text.

### Social Media

Ask if they have social media profiles. Configure the links in the theme or via widget/plugin. Verify that Open Graph is properly configured (via SEO plugin).

### Robots.txt and Sitemap

Verify that the XML sitemap is generated correctly. Verify robots.txt. If there are pages that should not be indexed (legal pages, thank-you pages...), set them to noindex.

---

## Phase 13 — Final Review

Before deactivating maintenance mode, review everything:

- All pages have content, a featured image, and complete SEO
- The menu works and all pages are accessible
- Forms send correctly (run a test)
- Legal pages are in the footer
- The cookie banner works
- The site looks good on mobile (responsive)
- Loading speed is acceptable
- Security and backup are active and configured
- Analytics records data correctly
- The sitemap is accessible
- No sample content remains
- Contact information is correct
- Open Graph looks good when sharing a URL
- (If e-commerce) The purchase process works end to end
- (If e-commerce) Transactional emails arrive correctly

### Search Engine Indexing

Before going live, ask the user: "Do you want search engines to index your site now?"

- If **yes:** disable "Discourage search engines from indexing this site" in Settings > Reading. Verify that robots.txt does not block crawlers and that the XML sitemap is accessible.
- If **not yet:** keep the option enabled. Remind the user they must disable it manually when they are ready for the site to appear in search results.

When everything is approved by the user, **deactivate maintenance mode**. The site is live.
