# WordPress Security Measures Catalog

## Complete Reference of 23 Security Measures

### 🟢 SAFE Measures (No side effects)

| # | ID | Measure | Points | Implementation |
|---|-----|---------|--------|----------------|
| 2.1 | `file_edit_disabled` | Disable file editing from dashboard | 5 | wp-config.php: `DISALLOW_FILE_EDIT` |
| 2.4 | `wpconfig_htaccess_protection` | Block HTTP access to wp-config.php | 5 | .htaccess: `<Files wp-config.php>` |
| 2.5 | `disable_directory_listing` | Disable directory listing | 5 | .htaccess: `Options -Indexes` |
| 2.6 | `uploads_php_execution_block` | Block PHP execution in uploads | 5 | .htaccess in wp-content/uploads/ |
| 2.7 | `sensitive_files_protection` | Block access to sensitive files | 4 | .htaccess: FilesMatch for .sql, .bak, .log |
| 2.9 | `login_attempt_limit` | Progressive brute force lockout | 10 | PHP: authenticate filter + transients |
| 2.12 | `disable_pingbacks_trackbacks` | Disable pingbacks/trackbacks | 3 | Options: default_ping_status = closed |
| 2.16 | `remove_pingback_header` | Remove X-Pingback header | 2 | PHP: wp_headers filter |
| 2.17 | `hotlinking_protection` | Block image hotlinking | 2 | .htaccess: RewriteCond/RewriteRule |
| 2.20 | `remove_version_info` | Remove WP version info | 3 | PHP: remove wp_generator, strip ?ver= |
| 2.21 | `idle_session_logout` | Auto-logout by inactivity | 3 | PHP: auth_cookie_expiration + JS timer |
| 2.22 | `weak_password_audit` | Audit weak passwords | 5 | PHP: wp_check_password against common list |

### 🟡 CAUTION Measures (May affect plugins/themes)

| # | ID | Measure | Points | Risk |
|---|-----|---------|--------|------|
| 2.2 | `xmlrpc_protection` | Block/limit XML-RPC | 8 | Jetpack, WP mobile app |
| 2.3 | `rest_api_protection` | Restrict REST API endpoints | 8 | Plugin API dependencies |
| 2.8 | `user_enumeration_protection` | Block user enumeration | 7 | Author archives → 404 |
| 2.10 | `force_ssl_admin` | Force HTTPS on admin | 10 | Breaks without valid SSL |
| 2.11 | `security_headers` | HTTP security headers | 7 | Variable per header |
| 2.14 | `custom_login_url` | Custom login URL | 3 | Users may lose access |
| 2.15 | `file_permissions_fix` | Fix file permissions | 5 | Server ACL conflicts |
| 2.18 | `disable_file_mods` | DISALLOW_FILE_MODS | — | Disables MCP abilities |

### 🔴 CRITICAL Measures (Can break the site)

| # | ID | Measure | Risk |
|---|-----|---------|------|
| 2.13 | `database_prefix_change` | Change DB prefix | SQL errors = site down |
| 2.19 | `move_wpconfig_outside` | Move wp-config.php | Site inaccessible |

### Non-Scoring Measures

| # | ID | Measure | Reason |
|---|-----|---------|--------|
| 2.13 | `database_prefix_change` | DB Prefix | 🔴 Too risky for scoring |
| 2.18 | `disable_file_mods` | File Mods | Incompatible with MCM |
| 2.19 | `move_wpconfig_outside` | Move wp-config | 🔴 Too risky for scoring |
| 2.23 | `force_logout_all` | Force Logout | Admin tool, not a measure |

## Security Score System

**Total possible: 100 points**

Score interpretation:
- **0-25:** Critical — Site is highly vulnerable
- **26-50:** Poor — Major improvements needed
- **51-75:** Moderate — Good base, some gaps remain
- **76-90:** Good — Well-hardened, minor improvements possible
- **91-100:** Excellent — Maximum hardening achieved
