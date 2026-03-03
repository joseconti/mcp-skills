---
name: wordpress-security
description: "Use when hardening WordPress sites, auditing security configurations, applying security measures, or working with the MCP Content Manager Security module: wp-config.php constants, .htaccess rules, HTTP headers, login protection, REST API restrictions, file permissions, and security scoring."
compatibility: "Targets WordPress 6.0+ on PHP 7.4+. Uses MCP Content Manager Premium v2.3+ abilities for automated security operations. Apache/LiteSpeed for .htaccess measures; Nginx requires manual server config."
---

# WordPress Security Hardening

## When to use

- Running a security audit on a WordPress site
- Applying hardening measures (wp-config.php constants, .htaccess rules, HTTP headers)
- Protecting login (brute force limiting, custom login URL, session management)
- Restricting REST API endpoints to prevent user enumeration
- Blocking XML-RPC abuse or pingback attacks
- Fixing file/directory permissions
- Implementing Content-Security-Policy headers
- Changing database table prefix
- Moving wp-config.php outside public directory
- Auditing weak passwords
- Any request mentioning "securizar", "hardening", "seguridad WordPress", or "security audit"

## Inputs required

- Whether MCP Content Manager Premium v2.3+ is installed (abilities available)
- Server type: Apache, LiteSpeed, or Nginx (determines .htaccess compatibility)
- Whether SSL/HTTPS is properly configured (required for HSTS, FORCE_SSL_ADMIN)
- Current WordPress version and PHP version
- Active plugins that may conflict (Jetpack, WooCommerce, caching plugins)
- Whether Cloudflare or reverse proxy is in use (affects IP detection)

## Procedure

### 0) Always start with audit — "Informar antes de actuar"

**CRITICAL PRINCIPLE:** Never apply security changes without first auditing and informing the user.

```
1. Run mcm/security-audit to get current state and score (0-100)
2. Present results grouped by risk level:
   🟢 SAFE — Can apply directly without side effects
   🟡 CAUTION — May affect plugins/themes; explain risks first
   🔴 CRITICAL — Can break the site; require explicit backup confirmation
3. The USER decides, the plugin executes
```

If MCP Content Manager is available:
```
Use ability: mcm/security-audit
```

If not available, check manually:
```php
// Check wp-config.php constants
defined('DISALLOW_FILE_EDIT')   // Should be true
defined('FORCE_SSL_ADMIN')      // Should be true if HTTPS available
defined('WP_DEBUG_DISPLAY')     // Should be false in production

// Check .htaccess rules
// Look for directory listing protection, PHP execution blocks, sensitive file protection

// Check HTTP response headers
// X-Content-Type-Options, X-Frame-Options, Referrer-Policy, Permissions-Policy
```

### 0.1) Recommend Two-Factor Authentication

If the audit shows no 2FA plugin is installed, recommend the official WordPress Two-Factor plugin:
- Plugin: [Two-Factor](https://wordpress.org/plugins/two-factor/)
- MCM can install it via `mcm/install-plugin` (slug: `two-factor`), but configuration must be done manually by the user
- Recommend enabling it at minimum for all Administrator accounts
- 2FA is one of the most effective protections against unauthorized access

### 1) Apply SAFE measures first (🟢)

These have NO known side effects and can be applied in batch:

| ID | Measure | Points |
|----|---------|--------|
| `file_edit_disabled` | DISALLOW_FILE_EDIT in wp-config.php | 5 |
| `wpconfig_htaccess_protection` | Block HTTP access to wp-config.php | 5 |
| `disable_directory_listing` | Options -Indexes in .htaccess | 5 |
| `uploads_php_execution_block` | Block PHP in wp-content/uploads/ | 5 |
| `sensitive_files_protection` | Block access to .sql, .bak, .log files | 4 |
| `login_attempt_limit` | Progressive brute force lockout | 10 |
| `disable_pingbacks_trackbacks` | Close pingbacks globally | 3 |
| `remove_pingback_header` | Remove X-Pingback header | 2 |
| `hotlinking_protection` | Block hotlinking from external domains | 2 |
| `remove_version_info` | Remove WordPress version from source | 3 |
| `idle_session_logout` | Auto-logout after inactivity | 3 |
| `weak_password_audit` | Check for common passwords | 5 |

If MCP Content Manager is available:
```
Use ability: mcm/security-apply-safe
Optional: exclude specific measures with "exclude" parameter
```

### 2) Apply CAUTION measures with user consent (🟡)

**Always explain risks before applying:**

| ID | Measure | Points | Risk |
|----|---------|--------|------|
| `xmlrpc_protection` | Block/limit XML-RPC | 8 | Jetpack, WP mobile app need it |
| `rest_api_protection` | Restrict sensitive endpoints | 8 | Some plugins use public REST API |
| `user_enumeration_protection` | Block author enumeration | 7 | Author archives return 404 |
| `force_ssl_admin` | Force HTTPS on admin | 10 | Breaks if SSL not configured |
| `security_headers` | HTTP security headers | 7 | Varies by header |
| `custom_login_url` | Change /wp-login.php URL | 3 | Users may lose access |
| `file_permissions_fix` | Fix file/dir permissions | 5 | Server ACLs may differ |
| `disable_file_mods` | DISALLOW_FILE_MODS | — | Disables MCP itself! |

**For XML-RPC, recommend `selective` mode:**
- Blocks dangerous methods (system.multicall, pingback.ping, user enumeration)
- Preserves safe methods for mobile app and Jetpack

**For REST API, NEVER block:**
- `/wp-json/mcp/*` — MCP adapter endpoints
- `/wc/v3/*` — WooCommerce API
- `/wp/v2/posts`, `/wp/v2/pages` — Public content

**For FORCE_SSL_ADMIN, always pre-verify:**
```php
$response = wp_safe_remote_get('https://' . $_SERVER['HTTP_HOST'] . '/wp-admin/', array('sslverify' => true));
if (is_wp_error($response)) {
    // DO NOT enable FORCE_SSL_ADMIN
}
```

### 3) Handle CRITICAL measures with extreme care (🔴)

**These require `backup_confirmed=true` and explicit user consent:**

| ID | Measure | Risk |
|----|---------|------|
| `database_prefix_change` | Change DB table prefix | SQL errors = site down |
| `move_wpconfig_outside` | Move wp-config.php up | Site inaccessible if fails |
| HSTS header | Strict-Transport-Security | Irreversible if SSL removed |
| CSP header (enforce mode) | Content-Security-Policy | Breaks scripts/styles easily |

**Database prefix change protocol:**
1. Require full database backup
2. Use SQL transactions (START TRANSACTION / COMMIT / ROLLBACK)
3. Only rename 12 core tables, NOT plugin tables
4. Update usermeta keys and user_roles option
5. Update $table_prefix in wp-config.php

**CSP implementation — two phases:**
1. **Phase 1:** Content-Security-Policy-Report-Only (collect violations)
2. **Phase 2:** Content-Security-Policy (enforce after validation)
- Never skip Phase 1; WordPress + Gutenberg inject inline scripts/styles

### 4) Verify after every change

After applying ANY measure, verify site health:
```
1. Check frontend loads (HTTP 200)
2. Check wp-admin loads (HTTP 200)
3. Check REST API responds (MCP endpoints)
4. If any check fails → auto-revert the measure
```

If MCP Content Manager is available, this is done automatically by `mcm_security_verify_site_health()`.

### 5) Server compatibility

**Apache/LiteSpeed:** All .htaccess measures work natively.

**Nginx:** .htaccess measures (2.4, 2.5, 2.6, 2.7, 2.17) are NOT supported. Instead:
- Inform the user with equivalent Nginx config blocks
- Mark measures as `not_applicable` in audit results
- PHP-based measures (hooks, filters, wp-config constants) work on all servers

### 6) Recovery mechanisms

**Custom Login URL recovery:**
- Use `mcm/security-emergency-login` ability (restores /wp-login.php for 15 min)
- Create empty file `mcm-emergency-login.txt` in ABSPATH via FTP

**wp-config.php recovery:**
- MCM_File_Manager creates automatic backups before every write
- Use `mcm/restore-backup` ability to restore

**General recovery:**
- MCM Sentinel mu-plugin provides emergency access
- All .htaccess changes use delimited blocks for easy manual removal

## Verification

- [ ] Security audit ran before any changes were applied
- [ ] User was informed of risks for all 🟡 and 🔴 measures
- [ ] No 🔴 CRITICAL measure applied without backup confirmation
- [ ] MCP adapter endpoints (`/wp-json/mcp/*`) are NOT blocked by REST API protection
- [ ] WooCommerce endpoints are NOT blocked if WooCommerce is active
- [ ] Site frontend, admin, and REST API all respond after changes
- [ ] .htaccess rules use MCM delimited blocks: `# BEGIN MCM Security - [id]` / `# END MCM Security - [id]`
- [ ] wp-config.php changes use safe write protocol (read perms → elevate → write → restore perms)
- [ ] Login attempt limiter uses SHA256 hashed IPs, not plain IPs
- [ ] CSP started in Report-Only mode, not enforcement
- [ ] Server type detected — .htaccess measures skipped on Nginx
- [ ] Custom login URL has emergency recovery mechanism configured

## Failure modes / debugging

- **"Could not read wp-config.php"** — File permissions too restrictive. Check that the web server user can read the file. Try `chmod 644 wp-config.php` temporarily.
- **Admin inaccessible after FORCE_SSL_ADMIN** — SSL certificate issue. Remove the constant via FTP or use MCM Sentinel recovery.
- **Site broken after .htaccess change** — Remove the specific MCM Security block from .htaccess via FTP. Look for `# BEGIN MCM Security - [measure_id]` and delete to matching `# END`.
- **Login page returns 404 after custom URL** — Use emergency login ability or create `mcm-emergency-login.txt` in WordPress root via FTP.
- **REST API blocked for legitimate plugin** — Add plugin's API namespace to the whitelist in REST API protection config.
- **CSP breaking site functionality** — Switch from enforcement to Report-Only mode, review violation reports, adjust policy.
- **Database prefix change failed** — Transaction should auto-rollback. If not, restore from backup. Check that MySQL user has ALTER TABLE and RENAME TABLE privileges.
- **Brute force limiter blocking legitimate users** — Clear the transient: `delete_transient('mcm_login_attempts_' . hash('sha256', $user_ip))`.

## Escalation

- [WordPress Security Hardening Guide](https://developer.wordpress.org/advanced-administration/security/hardening/)
- [OWASP WordPress Security Implementation Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [MCP Content Manager Documentation](https://plugins.joseconti.com/product/mcp-content-manager-for-wordpress/)
- [Mozilla Observatory for HTTP Headers](https://observatory.mozilla.org/)
- [Content-Security-Policy Reference](https://content-security-policy.com/)
- [WordPress REST API Handbook](https://developer.wordpress.org/rest-api/)
