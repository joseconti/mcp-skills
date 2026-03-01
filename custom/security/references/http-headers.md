# HTTP Security Headers Reference

## Headers by Risk Level

### 🟢 SAFE Headers (No side effects)

#### X-Content-Type-Options
```
X-Content-Type-Options: nosniff
```
Prevents MIME type sniffing. No known side effects.

#### Referrer-Policy
```
Referrer-Policy: strict-origin-when-cross-origin
```
Limits referrer information sent to external sites. No known side effects.

### 🟡 CAUTION Headers

#### X-Frame-Options
```
X-Frame-Options: SAMEORIGIN
```
Prevents clickjacking by blocking iframe embedding. **Risk:** Plugins that use iframes (e.g., payment gateways with 3D Secure) may break.

#### Permissions-Policy
```
Permissions-Policy: camera=(), microphone=(), geolocation=()
```
Restricts browser API access. **Risk:** Plugins using geolocation, camera, or microphone will fail.

### 🔴 CRITICAL Headers

#### Strict-Transport-Security (HSTS)
```
Strict-Transport-Security: max-age=31536000; includeSubDomains
```
Forces HTTPS for 1 year. **IRREVERSIBLE** — browsers cache this header. If SSL is removed, site becomes inaccessible for the cached duration. **Never enable without permanent SSL commitment.**

#### Content-Security-Policy (CSP)
```
Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data:;
```
Controls which resources can load. **Very easy to break WordPress functionality.** WordPress core, Gutenberg, and most plugins inject inline scripts/styles.

## CSP Implementation Guide

### Phase 1: Report-Only (MANDATORY first step)
```php
header("Content-Security-Policy-Report-Only: default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self' data:; connect-src 'self'; report-uri /wp-json/mcm/v1/csp-report");
```

### Phase 2: Enforcement (After reviewing reports)
```php
header("Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self' data:; connect-src 'self'");
```

### WordPress-Specific CSP Notes
- `'unsafe-inline'` is needed for styles (Gutenberg, customizer, most themes)
- `data:` is needed for img-src (inline images, SVGs)
- `https:` for img-src allows external images (CDN, Gravatar)
- Never use `'unsafe-eval'` unless absolutely required by a specific plugin
- For Google Analytics: add `https://www.google-analytics.com https://www.googletagmanager.com` to script-src
- For Google Fonts: add `https://fonts.googleapis.com` to style-src and `https://fonts.gstatic.com` to font-src

## Implementation Hook

```php
add_action('send_headers', function() {
    $config = get_option('mcm_security_headers_config', array());

    if (!empty($config['x_content_type_options'])) {
        header('X-Content-Type-Options: nosniff');
    }
    if (!empty($config['x_frame_options'])) {
        header('X-Frame-Options: SAMEORIGIN');
    }
    if (!empty($config['referrer_policy'])) {
        header('Referrer-Policy: strict-origin-when-cross-origin');
    }
    if (!empty($config['permissions_policy'])) {
        header('Permissions-Policy: camera=(), microphone=(), geolocation=()');
    }
    if (!empty($config['hsts'])) {
        header('Strict-Transport-Security: max-age=31536000; includeSubDomains');
    }
    if (!empty($config['csp'])) {
        $policy = get_option('mcm_security_csp_policy', "default-src 'self'");
        $header_name = !empty($config['csp_report_only'])
            ? 'Content-Security-Policy-Report-Only'
            : 'Content-Security-Policy';
        header($header_name . ': ' . $policy);
    }
}, 10);
```

**IMPORTANT:** Use `send_headers` action, NOT `wp_head`. Headers must be sent before any output.
