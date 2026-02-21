# HPOS Compatibility (High-Performance Order Storage)

Since WooCommerce 9.0, HPOS (custom order tables) is the default storage engine for orders. Orders are stored in `wp_wc_orders` and `wp_wc_orders_meta` instead of `wp_posts` and `wp_postmeta`.

## Golden rule

**Never use `WP_Query`, `get_posts()`, or direct `$wpdb` queries against `wp_posts`/`wp_postmeta` for orders.**

## Safe APIs

### Querying orders

```php
// CORRECT — works with both HPOS and legacy storage
$orders = wc_get_orders( array(
    'status'       => array( 'wc-completed', 'wc-processing' ),
    'limit'        => 50,
    'page'         => 1,
    'orderby'      => 'date',
    'order'        => 'DESC',
    'customer_id'  => $user_id,
    'date_created' => '>' . strtotime( '-30 days' ),
) );

// WRONG — will fail on HPOS stores
$orders = get_posts( array(
    'post_type'   => 'shop_order',
    'post_status' => 'wc-completed',
) );
```

### Reading order data

```php
$order = wc_get_order( $order_id );

// Use getter methods — never access properties directly
$total    = $order->get_total();
$status   = $order->get_status();
$email    = $order->get_billing_email();
$items    = $order->get_items();
$customer = $order->get_customer_id();
$date     = $order->get_date_created();
$meta     = $order->get_meta( '_custom_field' );
```

### Writing order data

```php
$order = wc_get_order( $order_id );

$order->set_status( 'completed' );
$order->set_billing_email( $new_email );
$order->update_meta_data( '_custom_field', $value );
$order->save(); // CRITICAL — always call save()
```

### Creating orders

```php
$order = wc_create_order( array(
    'customer_id' => $user_id,
    'status'      => 'pending',
) );

$order->add_product( wc_get_product( $product_id ), $quantity );
$order->set_address( $billing_address, 'billing' );
$order->set_address( $shipping_address, 'shipping' );
$order->calculate_totals();
$order->save();
```

## Declaring HPOS compatibility in your plugin

```php
add_action( 'before_woocommerce_init', function() {
    if ( class_exists( \Automattic\WooCommerce\Utilities\FeaturesUtil::class ) ) {
        \Automattic\WooCommerce\Utilities\FeaturesUtil::declare_compatibility(
            'custom_order_tables',
            __FILE__,
            true
        );
    }
} );
```

Without this declaration, WooCommerce will show a warning that your plugin is not HPOS-compatible.

## Custom meta queries

If you need custom queries on order meta:

```php
// CORRECT — use wc_get_orders with meta_query
$orders = wc_get_orders( array(
    'meta_query' => array(
        array(
            'key'   => '_payment_method',
            'value' => 'stripe',
        ),
    ),
) );

// For complex queries, use OrdersTableQuery (WC 8.0+)
use Automattic\WooCommerce\Internal\DataStores\Orders\OrdersTableQuery;

$query = new OrdersTableQuery( array(
    'field_query' => array(
        array(
            'field' => 'billing_email',
            'value' => 'test@example.com',
        ),
    ),
) );
$order_ids = $query->orders;
```

## Batch processing pattern

For processing large numbers of orders, always paginate:

```php
$page = 1;
do {
    $orders = wc_get_orders( array(
        'limit'  => 200,
        'page'   => $page,
        'status' => 'completed',
    ) );

    foreach ( $orders as $order ) {
        // Process each order.
    }

    ++$page;
} while ( count( $orders ) === 200 );
```
