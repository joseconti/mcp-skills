# Login Protection Reference

## Brute Force Rate Limiting

### Progressive Lockout Schedule
```
5 failed attempts  → 15 minutes lockout
10 failed attempts → 1 hour lockout
20 failed attempts → 24 hours lockout
```

### Storage: WordPress Transients
```php
$ip_hash = hash('sha256', $ip);
$transient_key = 'mcm_login_attempts_' . $ip_hash;
set_transient($transient_key, $attempts, 24 * HOUR_IN_SECONDS);
```

### IP Detection (Proxy-Aware)
```php
function mcm_security_get_ip() {
    $trusted_proxies = get_option('mcm_security_trusted_proxies', array());

    // Cloudflare — only trust if REMOTE_ADDR is a Cloudflare IP
    if (!empty($_SERVER['HTTP_CF_CONNECTING_IP']) && mcm_is_cloudflare_ip($_SERVER['REMOTE_ADDR'])) {
        $ip = $_SERVER['HTTP_CF_CONNECTING_IP'];
    }
    // Trusted proxy — only trust X-Forwarded-For from known proxies
    elseif (!empty($_SERVER['HTTP_X_FORWARDED_FOR']) && in_array($_SERVER['REMOTE_ADDR'], $trusted_proxies, true)) {
        $ip = explode(',', $_SERVER['HTTP_X_FORWARDED_FOR'])[0];
    }
    // Direct connection
    else {
        $ip = $_SERVER['REMOTE_ADDR'];
    }

    return filter_var(trim($ip), FILTER_VALIDATE_IP) ?: $_SERVER['REMOTE_ADDR'];
}
```

### Timing Attack Prevention
```php
// Make invalid username attempts take same time as valid ones
add_filter('authenticate', function($user, $username, $password) {
    if (is_wp_error($user) && $user->get_error_code() === 'invalid_username') {
        wp_hash_password('timing-safe-padding-' . wp_generate_password(12));
    }
    return $user;
}, 100, 3);
```

### Honeypot Bot Detection
```php
// Hidden field in login form — bots fill it, humans don't
add_action('login_form', function() {
    echo '<p style="display:none !important;position:absolute;left:-9999px;">
        <label for="mcm_hp_field">Leave empty</label>
        <input type="text" name="mcm_hp_field" id="mcm_hp_field" value="" autocomplete="off" tabindex="-1" />
    </p>';
});
```

## Custom Login URL

### Configuration
- Stored in option: `mcm_security_login_slug`
- Uses WordPress rewrite rules
- Filters `login_url`, `site_url`, and `wp_mail` to update URLs

### Emergency Recovery
1. **MCP Ability:** `mcm/security-emergency-login` — sets transient for 15 min
2. **FTP Method:** Create empty file `mcm-emergency-login.txt` in ABSPATH
3. Both methods temporarily restore /wp-login.php access

### Implementation Hooks
```php
// Priority 1 — rewrite rule
add_action('init', 'register_custom_login_rewrite', 1);

// Priority 9 — block original wp-login.php (before WP auth)
add_action('template_redirect', 'block_original_login', 9);

// Priority 10 — filter login URLs
add_filter('login_url', 'filter_login_url', 10, 2);
add_filter('site_url', 'filter_site_url', 10, 3);
add_filter('wp_mail', 'filter_mail_login_urls');
```

## Session Management

### Idle Logout
```php
add_filter('auth_cookie_expiration', function($expiration, $user_id, $remember) {
    $timeouts = get_option('mcm_security_idle_timeout', array(
        'administrator' => 30,  // minutes
        'editor' => 60,
    ));
    // Match user's highest role to timeout
}, 10, 3);
```

### JavaScript Activity Monitor
File: `assets/js/idle-logout.js`
- Monitors mousemove, keypress, click events
- Redirects to login after configured idle time
- Uses `mcmIdleLogout.idleTimeout` (milliseconds) from `wp_localize_script`

### Force Logout All
```php
// Destroy all sessions except current user (optional)
$sessions = WP_Session_Tokens::get_instance($user_id);
$sessions->destroy_all();
```
**NOTE:** Does NOT affect MCP token-based connections (OAuth).
