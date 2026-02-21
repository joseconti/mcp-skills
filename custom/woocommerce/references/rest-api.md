# WooCommerce REST API

Extending and working with the WooCommerce REST API (v3).

## Base URL

```
/wp-json/wc/v3/
```

## Authentication

WooCommerce REST API supports:
1. **Consumer key/secret** — For external applications (Basic Auth or query params)
2. **Cookie + nonce** — For authenticated WordPress users (same as WP REST API)
3. **Application Passwords** — WordPress 5.6+ (for external tools)

```php
// Consumer key/secret in request header.
Authorization: Basic base64_encode( consumer_key:consumer_secret )

// Or as query params (HTTPS only).
https://example.com/wp-json/wc/v3/orders?consumer_key=ck_xxx&consumer_secret=cs_xxx
```

## Core endpoints

| Resource | Endpoint | Methods |
|---------|----------|---------|
| Products | `/wc/v3/products` | GET, POST, PUT, DELETE |
| Product Variations | `/wc/v3/products/{id}/variations` | GET, POST, PUT, DELETE |
| Orders | `/wc/v3/orders` | GET, POST, PUT, DELETE |
| Customers | `/wc/v3/customers` | GET, POST, PUT, DELETE |
| Coupons | `/wc/v3/coupons` | GET, POST, PUT, DELETE |
| Reports | `/wc/v3/reports/sales` | GET |
| Settings | `/wc/v3/settings/{group}` | GET, PUT |
| Shipping Zones | `/wc/v3/shipping/zones` | GET, POST, PUT, DELETE |
| Payment Gateways | `/wc/v3/payment_gateways` | GET, PUT |
| Tax Rates | `/wc/v3/taxes` | GET, POST, PUT, DELETE |

## Adding custom fields to existing endpoints

```php
// Add a custom field to the product REST response.
add_filter( 'woocommerce_rest_prepare_product_object', function( $response, $product, $request ) {
    $response->data['custom_field'] = $product->get_meta( '_custom_field' );
    return $response;
}, 10, 3 );

// Save the custom field when product is updated via REST.
add_action( 'woocommerce_rest_insert_product_object', function( $product, $request, $creating ) {
    if ( isset( $request['custom_field'] ) ) {
        $product->update_meta_data( '_custom_field', wc_clean( $request['custom_field'] ) );
        $product->save();
    }
}, 10, 3 );
```

## Creating a custom endpoint

```php
// Method 1: Using WooCommerce's REST controller registration.
add_filter( 'woocommerce_rest_api_get_rest_namespaces', function( $controllers ) {
    $controllers['wc/v3']['my-resource'] = 'My_REST_Controller';
    return $controllers;
} );

class My_REST_Controller extends WC_REST_Controller {

    protected $namespace = 'wc/v3';
    protected $rest_base = 'my-resource';

    public function register_routes() {
        register_rest_route( $this->namespace, '/' . $this->rest_base, array(
            array(
                'methods'             => WP_REST_Server::READABLE,
                'callback'            => array( $this, 'get_items' ),
                'permission_callback' => array( $this, 'get_items_permissions_check' ),
            ),
        ) );
    }

    public function get_items_permissions_check( $request ) {
        return current_user_can( 'manage_woocommerce' );
    }

    public function get_items( $request ) {
        // Return your data.
        return rest_ensure_response( array( 'data' => array() ) );
    }
}

// Method 2: Simple register_rest_route (for lightweight endpoints).
add_action( 'rest_api_init', function() {
    register_rest_route( 'my-plugin/v1', '/wc-data', array(
        'methods'             => 'GET',
        'callback'            => 'my_wc_data_callback',
        'permission_callback' => function() {
            return current_user_can( 'manage_woocommerce' );
        },
    ) );
} );
```

## Pagination

WooCommerce REST API supports pagination via headers:

```
X-WP-Total: 120        (total items)
X-WP-TotalPages: 12    (total pages)
```

Query params: `per_page` (max 100), `page`, `offset`.

## Filtering

Common filter parameters for list endpoints:

```
# Products
?status=publish&category=15&on_sale=true&min_price=10&max_price=100&sku=ABC123

# Orders
?status=completed&customer=5&after=2024-01-01T00:00:00&before=2024-12-31T23:59:59

# Customers
?role=customer&email=test@example.com&orderby=registered_date
```

## Webhooks

WooCommerce has built-in webhook support (Settings > Advanced > Webhooks):

Topics: `order.created`, `order.updated`, `order.deleted`, `product.created`, `product.updated`, `customer.created`, `coupon.created`, etc.

Programmatic webhook creation:

```php
$webhook = new WC_Webhook();
$webhook->set_name( 'Order completed' );
$webhook->set_topic( 'order.completed' );
$webhook->set_delivery_url( 'https://example.com/webhook' );
$webhook->set_secret( wp_generate_password( 50, true, true ) );
$webhook->set_status( 'active' );
$webhook->save();
```
