# WooCommerce Security

Security patterns specific to WooCommerce development. These supplement the general WordPress security rules.

## Capabilities

WooCommerce defines its own capabilities:

| Capability | Who has it | Use for |
|-----------|-----------|---------|
| `manage_woocommerce` | Shop Manager, Administrator | Store settings, all orders, all products |
| `edit_shop_orders` | Shop Manager, Administrator | Order CRUD |
| `edit_products` | Shop Manager, Administrator | Product CRUD |
| `view_woocommerce_reports` | Shop Manager, Administrator | Analytics and reports |
| `edit_others_shop_orders` | Shop Manager, Administrator | Other users' orders |

```php
// Admin-level WooCommerce operations.
if ( ! current_user_can( 'manage_woocommerce' ) ) {
    return new WP_Error( 'forbidden', 'Insufficient permissions.', array( 'status' => 403 ) );
}

// Customer viewing own orders.
$order = wc_get_order( $order_id );
if ( $order->get_customer_id() !== get_current_user_id() ) {
    return new WP_Error( 'forbidden', 'You cannot view this order.', array( 'status' => 403 ) );
}
```

## Sanitization

WooCommerce provides its own sanitization functions:

```php
// General text cleanup (strips tags, trims, removes extra whitespace).
$clean = wc_clean( $input );

// Textarea (preserves line breaks).
$clean = wc_sanitize_textarea( $input );

// Tooltip text.
$clean = wc_sanitize_tooltip( $input );

// For prices — use WC formatting.
$price = wc_format_decimal( $input );

// For boolean values from checkboxes.
$bool = wc_string_to_bool( $input );
```

## Never expose sensitive data

### Payment credentials

```php
// WRONG — exposes API keys in REST responses.
return array(
    'gateway'    => $this->id,
    'api_key'    => $this->get_option( 'api_key' ),
    'secret_key' => $this->get_option( 'secret_key' ),
);

// CORRECT — only return non-sensitive info.
return array(
    'gateway' => $this->id,
    'title'   => $this->title,
    'enabled' => $this->enabled,
);
```

### Customer PII (Personally Identifiable Information)

```php
// WRONG — full email in public-facing output.
echo $order->get_billing_email();

// CORRECT — mask sensitive data.
$email = $order->get_billing_email();
$parts = explode( '@', $email );
echo substr( $parts[0], 0, 2 ) . '***@' . $parts[1];
```

### Order notes

```php
// Customer-visible note — never include internal details.
$order->add_order_note( 'Your order has been shipped.', true ); // true = customer note

// Internal-only note — can include details.
$order->add_order_note( 'Gateway transaction ID: ' . $txn_id, false ); // false = private
```

## Nonces in WooCommerce context

WooCommerce has its own nonce patterns:

```php
// Checkout nonce (auto-handled by WC).
// Verified internally by WooCommerce — don't duplicate.

// Custom AJAX endpoints.
add_action( 'wp_ajax_my_wc_action', function() {
    check_ajax_referer( 'my-wc-nonce', 'security' );
    // ... process ...
    wp_send_json_success();
} );

// Custom admin actions.
if ( ! wp_verify_nonce( $_POST['_wpnonce'], 'my_wc_admin_action' ) ) {
    wp_die( 'Security check failed.' );
}
```

## Webhook security

When receiving webhooks from payment gateways:

```php
// ALWAYS verify the webhook signature.
$payload   = file_get_contents( 'php://input' );
$signature = $_SERVER['HTTP_X_GATEWAY_SIGNATURE'] ?? '';
$expected  = hash_hmac( 'sha256', $payload, $this->get_option( 'webhook_secret' ) );

if ( ! hash_equals( $expected, $signature ) ) {
    status_header( 401 );
    exit;
}
```

## SQL injection in WooCommerce

Even with HPOS, you might need custom queries for reporting:

```php
// WRONG.
$results = $wpdb->get_results(
    "SELECT * FROM {$wpdb->prefix}wc_orders WHERE billing_email = '$email'"
);

// CORRECT.
$results = $wpdb->get_results(
    $wpdb->prepare(
        "SELECT * FROM {$wpdb->prefix}wc_orders WHERE billing_email = %s",
        $email
    )
);
```

## Rate limiting for WooCommerce REST API

The WC REST API uses consumer key/secret authentication. For custom public endpoints, add rate limiting:

```php
public function permission_callback( $request ) {
    $ip    = $request->get_header( 'x-forwarded-for' ) ?: $_SERVER['REMOTE_ADDR'];
    $key   = 'wc_rate_' . md5( $ip );
    $count = (int) get_transient( $key );

    if ( $count > 100 ) {
        return new WP_Error( 'rate_limited', 'Too many requests.', array( 'status' => 429 ) );
    }

    set_transient( $key, $count + 1, MINUTE_IN_SECONDS );
    return true;
}
```
