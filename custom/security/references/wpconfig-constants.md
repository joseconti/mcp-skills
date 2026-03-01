# wp-config.php Security Constants Reference

## Core Security Constants

### DISALLOW_FILE_EDIT (🟢 SAFE)
```php
define('DISALLOW_FILE_EDIT', true);
```
Disables the Theme Editor and Plugin Editor in wp-admin. Does NOT prevent plugin/theme updates or installations.

### DISALLOW_FILE_MODS (🟡 CAUTION)
```php
define('DISALLOW_FILE_MODS', true);
```
Disables ALL file modifications: plugin/theme editor, updates, and installations. **WARNING:** This also disables MCP Content Manager's file management abilities. Only use in CI/CD environments.

### FORCE_SSL_ADMIN (🟡 CAUTION)
```php
define('FORCE_SSL_ADMIN', true);
```
Forces HTTPS on the admin panel. **Pre-verification required:** Must confirm HTTPS works before enabling.

### WP_DEBUG (Production Settings)
```php
define('WP_DEBUG', false);
define('WP_DEBUG_LOG', false);
define('WP_DEBUG_DISPLAY', false);
@ini_set('display_errors', 0);
define('SCRIPT_DEBUG', false);
```
Production sites must have debug disabled and display_errors off.

## Additional Security Constants (Optional)

### Session and Cookie Security
```php
define('FORCE_SSL_LOGIN', true);     // Force SSL on login page
define('COOKIE_DOMAIN', $_SERVER['HTTP_HOST']); // Restrict cookie domain
```

### Content Management
```php
define('AUTOSAVE_INTERVAL', 300);    // 5 min (default 60s) — reduces XSS surface
define('WP_POST_REVISIONS', 5);     // Limit revisions (reduces DB size)
define('EMPTY_TRASH_DAYS', 7);      // Auto-empty trash (default 30 days)
```

### External Request Control
```php
define('WP_HTTP_BLOCK_EXTERNAL', true);
define('WP_ACCESSIBLE_HOSTS', 'api.wordpress.org,downloads.wordpress.org');
```
**WARNING:** Blocks all outgoing HTTP requests except whitelisted hosts. Can break plugins that call external APIs.

## Safe Write Protocol

When modifying wp-config.php programmatically:

```php
// 1. Read current permissions
$original_perms = @fileperms($wpconfig_path);

// 2. Elevate to 644 if needed
if (decoct($original_perms & 0777) < 644) {
    @chmod($wpconfig_path, 0644);
}

// 3. Write changes via MCM_File_Manager (auto-backup)
MCM_File_Manager::write_file('wp-config.php', $new_content);

// 4. Restore original permissions
@chmod($wpconfig_path, $original_perms);

// 5. Verify restoration
$restored = @fileperms($wpconfig_path);
assert($restored === $original_perms);
```

## Insertion Anchors

When adding new constants, insert before these markers (in order of preference):

1. `/* That's all, stop editing! Happy publishing. */`
2. `/* That's all, stop editing! Happy blogging. */`
3. `/** Absolute path to the WordPress directory. */`
4. `require_once ABSPATH . 'wp-settings.php';`

## Recommended File Permissions

```
wp-config.php:  400 (r--------) or 440 (r--r-----)
.htaccess:      644 (rw-r--r--)
Directories:    755 (rwxr-xr-x)
PHP files:      644 (rw-r--r--)
```
