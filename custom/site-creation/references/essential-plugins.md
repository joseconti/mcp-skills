# Phase 5: Essential Plugins

For each category, offer options and let the user choose. Do not install without asking.

---

## 5.1 Security

Options: Wordfence Security, Solid Security, Sucuri Security.

Minimum configuration: basic firewall, login protection, login attempt limits.

## 5.2 Backups

Options: UpdraftPlus, BackWPup, Duplicator.

Configuration: automatic weekly backup at minimum. Ask where to store backups (Google Drive, Dropbox, server, etc.).

## 5.3 Cache & Performance

Options: LiteSpeed Cache (if the server is LiteSpeed), WP Super Cache, W3 Total Cache, WP Fastest Cache.

Ask: "Do you know what web server your hosting uses? (Apache, Nginx, LiteSpeed)" to recommend the best option.

## 5.4 Anti-Spam

Options: Akismet Anti-Spam, Antispam Bee, CleanTalk.

## 5.5 Contact Form

Options: Contact Form 7, WPForms Lite, Fluent Forms, Forminator.

This plugin is needed for the contact page to work. Without it, the page has no form.

## 5.6 Email (SMTP)

WordPress by default does not send emails reliably; many end up in spam or simply don't arrive. An SMTP plugin is almost mandatory for forms and notifications to work.

Options: WP Mail SMTP, FluentSMTP, Post SMTP.

Ask: "Do you have SMTP server credentials? (Gmail, your hosting, SendGrid, etc.)"

## 5.7 Cookie Consent (GDPR)

A cookie policy page alone is not enough. A **functional banner** is needed that blocks cookies until the user accepts and allows managing preferences by category.

Options: CookieYes, Complianz, GDPR Cookie Consent (WebToffee).

Configuration: cookie categories, banner text, link to the cookie policy page.

## 5.8 Analytics

Ask: "Do you want to install an analytics system?"

If yes, offer options:

- **Google Site Kit** — integrates Analytics, Search Console, and more. Ideal for the Google ecosystem.
- **MonsterInsights** — simple Google Analytics integration.
- **Matomo Analytics** — open source alternative, data hosted on your server.
- **Plausible Analytics** — lightweight, privacy-friendly, no cookies.
- **Manual setup** — insert tracking code via theme or code insertion plugin.

Ask if they already have an account with any service and whether they prefer a cookieless option.

Minimum configuration: connect the account, verify it records data, exclude admin traffic.

## 5.9 Multilingual (if applicable)

Only if the user indicated they need multiple languages: WPML (paid), Polylang, TranslatePress.
