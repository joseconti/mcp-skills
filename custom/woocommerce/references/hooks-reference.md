# WooCommerce Hooks Reference

Essential hooks organized by lifecycle stage.

## Product hooks

### Admin product editing
| Hook | Type | When |
|------|------|------|
| `woocommerce_product_options_general_product_data` | action | General tab in product editor |
| `woocommerce_product_options_inventory_product_data` | action | Inventory tab |
| `woocommerce_product_options_shipping_product_data` | action | Shipping tab |
| `woocommerce_product_options_advanced` | action | Advanced tab |
| `woocommerce_process_product_meta` | action | Product saved (receives `$post_id`) |
| `woocommerce_product_data_tabs` | filter | Add custom product data tabs |

### Product display
| Hook | Type | When |
|------|------|------|
| `woocommerce_before_single_product` | action | Before product page |
| `woocommerce_single_product_summary` | action | Product summary area (title, price, add-to-cart) |
| `woocommerce_after_single_product` | action | After product page |
| `woocommerce_get_price_html` | filter | Modify displayed price HTML |
| `woocommerce_product_get_price` | filter | Modify product price value |
| `woocommerce_is_purchasable` | filter | Control if product can be purchased |

## Cart hooks

| Hook | Type | When |
|------|------|------|
| `woocommerce_add_to_cart_validation` | filter | Before item added to cart (return false to prevent) |
| `woocommerce_add_to_cart` | action | After item added to cart |
| `woocommerce_before_cart` | action | Before cart table |
| `woocommerce_cart_calculate_fees` | action | Add custom fees to cart |
| `woocommerce_cart_item_price` | filter | Modify displayed cart item price |
| `woocommerce_calculated_total` | filter | Modify cart total |

## Checkout hooks

| Hook | Type | When |
|------|------|------|
| `woocommerce_before_checkout_form` | action | Before checkout form |
| `woocommerce_checkout_fields` | filter | Modify checkout fields |
| `woocommerce_checkout_process` | action | Validate custom checkout fields |
| `woocommerce_checkout_create_order` | action | Before order is created from checkout |
| `woocommerce_checkout_order_processed` | action | After order created, before payment |
| `woocommerce_checkout_update_order_meta` | action | Save custom checkout data to order |

## Order hooks

| Hook | Type | When |
|------|------|------|
| `woocommerce_new_order` | action | New order created (receives `$order_id`) |
| `woocommerce_payment_complete` | action | Payment completed (receives `$order_id`) |
| `woocommerce_order_status_changed` | action | Any status change (`$order_id, $old_status, $new_status`) |
| `woocommerce_order_status_{status}` | action | Specific status reached (`$order_id`) |
| `woocommerce_order_status_{from}_to_{to}` | action | Specific transition (`$order_id`) |
| `woocommerce_order_refunded` | action | Order refunded (`$order_id, $refund_id`) |

## Payment gateway hooks

| Hook | Type | When |
|------|------|------|
| `woocommerce_payment_gateways` | filter | Register payment gateways |
| `woocommerce_available_payment_gateways` | filter | Filter available gateways at checkout |
| `woocommerce_receipt_{gateway_id}` | action | Payment receipt page |
| `woocommerce_api_{gateway_id}` | action | IPN / webhook callback URL |

## Shipping hooks

| Hook | Type | When |
|------|------|------|
| `woocommerce_shipping_methods` | filter | Register shipping methods |
| `woocommerce_package_rates` | filter | Modify available shipping rates |
| `woocommerce_shipping_zone_before_methods_table` | action | Shipping zone admin |

## Email hooks

| Hook | Type | When |
|------|------|------|
| `woocommerce_email_classes` | filter | Register custom emails |
| `woocommerce_email_before_order_table` | action | Before order details in email |
| `woocommerce_email_after_order_table` | action | After order details in email |
| `woocommerce_email_order_meta` | action | Add custom data to order emails |

## REST API hooks

| Hook | Type | When |
|------|------|------|
| `woocommerce_rest_prepare_product_object` | filter | Modify product REST response |
| `woocommerce_rest_insert_product_object` | action | After product created/updated via REST |
| `woocommerce_rest_prepare_shop_order_object` | filter | Modify order REST response |
| `woocommerce_rest_check_permissions` | filter | Custom permission checks |

## Initialization hooks (load order)

1. `before_woocommerce_init` — Declare feature compatibility (HPOS, blocks)
2. `woocommerce_loaded` — WooCommerce fully loaded
3. `woocommerce_init` — WooCommerce initialized
4. `woocommerce_after_register_taxonomy` — Taxonomies registered
5. `woocommerce_after_register_post_type` — Post types registered
