---
name: woocommerce
description: "Use when developing WooCommerce extensions, customizing store behavior, or working with WooCommerce APIs: HPOS-compatible data access, product/order/customer APIs, hooks, payment gateways, shipping methods, emails, and REST API extensions."
compatibility: "Targets WooCommerce 9.0+ (HPOS era) on WordPress 6.9+ (PHP 7.4+). Uses WooCommerce's native abstraction layer for full HPOS compatibility."
---

# WooCommerce Development

## When to use

- Writing or modifying a WooCommerce extension (plugin)
- Working with orders, products, customers, or subscriptions programmatically
- Extending WooCommerce REST API endpoints
- Customizing checkout, cart, or payment flows
- Adding custom product types or order statuses
- Integrating with WooCommerce hooks and filters
- Building payment gateway or shipping method extensions

## Inputs required

- The WooCommerce version installed on the target site (9.0+ assumed)
- Whether HPOS (High-Performance Order Storage) is enabled (assume yes)
- Which WooCommerce APIs are relevant: orders, products, customers, subscriptions, settings

## Procedure

### 0) Verify WooCommerce context

Before writing any WooCommerce code:

1. Check that WooCommerce is active: `if ( ! class_exists( 'WooCommerce' ) ) return;`
2. Confirm HPOS compatibility — never query `wp_posts` directly for orders
3. Use `woocommerce_loaded` or `plugins_loaded` hooks for initialization

### 1) Use HPOS-compatible APIs exclusively

**CRITICAL:** WooCommerce 9.0+ uses HPOS (custom order tables) by default. Direct `$wpdb` queries against `wp_posts`/`wp_postmeta` for orders will BREAK on HPOS-enabled stores.

Safe API usage:
```php
// Orders — ALWAYS use wc_get_orders() or WC_Order_Query
$orders = wc_get_orders( array(
    'status'   => 'completed',
    'limit'    => 50,
    'orderby'  => 'date',
    'order'    => 'DESC',
) );

// Products — use wc_get_products() or wc_get_product()
$product = wc_get_product( $product_id );

// Customers — use WC_Customer class
$customer = new WC_Customer( $user_id );
```

See: `references/hpos-compatibility.md`

### 2) Follow WooCommerce hook patterns

WooCommerce provides hooks at every stage of the lifecycle. Use them instead of overriding templates or modifying core behavior.

Key hook categories:
- **Cart**: `woocommerce_before_cart`, `woocommerce_cart_calculate_fees`, `woocommerce_add_to_cart_validation`
- **Checkout**: `woocommerce_checkout_process`, `woocommerce_checkout_order_processed`, `woocommerce_payment_complete`
- **Orders**: `woocommerce_order_status_changed`, `woocommerce_new_order`, `woocommerce_order_refunded`
- **Products**: `woocommerce_product_options_general_product_data`, `woocommerce_process_product_meta`
- **Emails**: `woocommerce_email_classes`, `woocommerce_email_before_order_table`

See: `references/hooks-reference.md`

### 3) Extend properly — don't hack core

- **Payment gateways**: Extend `WC_Payment_Gateway`, implement `process_payment()`, register via `woocommerce_payment_gateways` filter
- **Shipping methods**: Extend `WC_Shipping_Method`, implement `calculate_shipping()`, register via `woocommerce_shipping_methods` filter
- **Emails**: Extend `WC_Email`, register via `woocommerce_email_classes` filter
- **Product types**: Extend `WC_Product`, register via `woocommerce_product_class` filter
- **Settings**: Use `WC_Settings_API` trait or add settings tabs via `woocommerce_get_settings_pages`

See: `references/extending-woocommerce.md`

### 4) Security for WooCommerce

- Use `current_user_can( 'manage_woocommerce' )` for admin-level WC operations
- Use `wc_clean()` and `wc_sanitize_textarea()` for WooCommerce-specific sanitization
- Never expose API keys, payment credentials, or customer PII in responses
- Use `$wpdb->prepare()` for any custom database queries
- Validate order ownership before exposing order data: `$order->get_customer_id() === get_current_user_id()`

See: `references/security.md`

### 5) REST API extensions

WooCommerce REST API (v3) is at `/wp-json/wc/v3/`. To extend it:

```php
add_filter( 'woocommerce_rest_api_get_rest_namespaces', function( $controllers ) {
    $controllers['wc/v3']['my-endpoint'] = 'My_REST_Controller';
    return $controllers;
} );
```

For custom fields on existing endpoints, use `woocommerce_rest_prepare_*` and `woocommerce_rest_insert_*` filters.

See: `references/rest-api.md`

## Verification

- [ ] No direct SQL queries against `wp_posts`/`wp_postmeta` for orders (HPOS-safe)
- [ ] All WC functions called after `woocommerce_loaded` or `plugins_loaded`
- [ ] WooCommerce existence check before any WC-dependent code
- [ ] Payment/shipping extensions use proper abstract class inheritance
- [ ] Customer PII is not exposed in logs, error messages, or API responses
- [ ] Custom order statuses registered via `wc_register_order_type` or `register_post_status` + `wc_order_statuses` filter

## Failure modes / debugging

- **"Call to undefined function wc_get_orders()"** — WooCommerce not loaded yet. Move code to `woocommerce_loaded` hook.
- **Orders not found** — HPOS migration may be incomplete. Check `wc_get_container()->get( OrdersTableDataStore::class )` status.
- **Payment gateway not appearing** — Check `is_available()` method, supported currencies, and `woocommerce_payment_gateways` filter priority.
- **Email not sending** — Check `WC_Emails::instance()`, verify template exists, check email is enabled in WooCommerce > Settings > Emails.

## Escalation

- [WooCommerce Developer Documentation](https://developer.woocommerce.com/docs/)
- [WooCommerce GitHub Issues](https://github.com/woocommerce/woocommerce/issues)
- [WooCommerce REST API Reference](https://woocommerce.github.io/woocommerce-rest-api-docs/)
