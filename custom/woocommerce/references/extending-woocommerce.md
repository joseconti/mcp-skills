# Extending WooCommerce

Patterns for building payment gateways, shipping methods, emails, and custom product types.

## Payment gateway

```php
class My_Gateway extends WC_Payment_Gateway {

    public function __construct() {
        $this->id                 = 'my_gateway';
        $this->method_title       = 'My Gateway';
        $this->method_description = 'Accept payments via My Gateway.';
        $this->has_fields         = true;
        $this->supports           = array( 'products', 'refunds' );

        $this->init_form_fields();
        $this->init_settings();

        $this->title   = $this->get_option( 'title' );
        $this->enabled = $this->get_option( 'enabled' );

        add_action( 'woocommerce_update_options_payment_gateways_' . $this->id, array( $this, 'process_admin_options' ) );
    }

    public function init_form_fields() {
        $this->form_fields = array(
            'enabled' => array(
                'title'   => 'Enable/Disable',
                'type'    => 'checkbox',
                'label'   => 'Enable My Gateway',
                'default' => 'no',
            ),
            'title' => array(
                'title'   => 'Title',
                'type'    => 'text',
                'default' => 'My Gateway',
            ),
        );
    }

    public function process_payment( $order_id ) {
        $order = wc_get_order( $order_id );

        // Process the payment...

        $order->payment_complete( $transaction_id );

        return array(
            'result'   => 'success',
            'redirect' => $this->get_return_url( $order ),
        );
    }

    public function process_refund( $order_id, $amount = null, $reason = '' ) {
        // Process refund via gateway API...
        return true; // or WP_Error on failure.
    }
}

// Register the gateway.
add_filter( 'woocommerce_payment_gateways', function( $gateways ) {
    $gateways[] = 'My_Gateway';
    return $gateways;
} );
```

## Shipping method

```php
class My_Shipping_Method extends WC_Shipping_Method {

    public function __construct( $instance_id = 0 ) {
        $this->id                 = 'my_shipping';
        $this->instance_id        = absint( $instance_id );
        $this->method_title       = 'My Shipping';
        $this->method_description = 'Custom shipping method.';
        $this->supports           = array( 'shipping-zones', 'instance-settings' );

        $this->init_form_fields();
        $this->init_settings();

        $this->title = $this->get_option( 'title' );
    }

    public function calculate_shipping( $package = array() ) {
        $rate = array(
            'id'    => $this->get_rate_id(),
            'label' => $this->title,
            'cost'  => 10.00,
        );
        $this->add_rate( $rate );
    }
}

add_filter( 'woocommerce_shipping_methods', function( $methods ) {
    $methods['my_shipping'] = 'My_Shipping_Method';
    return $methods;
} );
```

## Custom email

```php
class My_Custom_Email extends WC_Email {

    public function __construct() {
        $this->id             = 'my_custom_email';
        $this->title          = 'My Custom Email';
        $this->description    = 'Sent when something happens.';
        $this->heading        = 'Something happened';
        $this->subject        = 'Something happened on {site_title}';
        $this->template_html  = 'emails/my-custom-email.php';
        $this->template_plain = 'emails/plain/my-custom-email.php';
        $this->template_base  = plugin_dir_path( __FILE__ ) . 'templates/';

        // Trigger on a custom action.
        add_action( 'my_custom_trigger', array( $this, 'trigger' ), 10, 1 );

        parent::__construct();
    }

    public function trigger( $order_id ) {
        $this->object = wc_get_order( $order_id );
        if ( ! $this->object ) {
            return;
        }
        $this->recipient = $this->object->get_billing_email();
        $this->send(
            $this->get_recipient(),
            $this->get_subject(),
            $this->get_content(),
            $this->get_headers(),
            $this->get_attachments()
        );
    }

    public function get_content_html() {
        return wc_get_template_html(
            $this->template_html,
            array(
                'order'         => $this->object,
                'email_heading' => $this->get_heading(),
                'email'         => $this,
            ),
            '',
            $this->template_base
        );
    }
}

add_filter( 'woocommerce_email_classes', function( $emails ) {
    $emails['My_Custom_Email'] = new My_Custom_Email();
    return $emails;
} );
```

## Custom product type

```php
class WC_Product_Custom extends WC_Product {
    public function get_type() {
        return 'custom';
    }
}

// Register product type.
add_filter( 'woocommerce_product_class', function( $classname, $product_type ) {
    if ( 'custom' === $product_type ) {
        return 'WC_Product_Custom';
    }
    return $classname;
}, 10, 2 );

// Add to product type selector.
add_filter( 'product_type_selector', function( $types ) {
    $types['custom'] = 'Custom Product';
    return $types;
} );
```

## Custom order status

```php
// Register the status.
add_action( 'init', function() {
    register_post_status( 'wc-custom-status', array(
        'label'                     => 'Custom Status',
        'public'                    => true,
        'exclude_from_search'       => false,
        'show_in_admin_all_list'    => true,
        'show_in_admin_status_list' => true,
        'label_count'               => _n_noop( 'Custom (%s)', 'Custom (%s)' ),
    ) );
} );

// Add to WooCommerce order statuses.
add_filter( 'wc_order_statuses', function( $statuses ) {
    $statuses['wc-custom-status'] = 'Custom Status';
    return $statuses;
} );
```

## Settings tab

```php
class My_Settings extends WC_Settings_Page {

    public function __construct() {
        $this->id    = 'my_settings';
        $this->label = 'My Settings';
        parent::__construct();
    }

    public function get_settings() {
        return array(
            array(
                'title' => 'My Settings Section',
                'type'  => 'title',
                'id'    => 'my_settings_section',
            ),
            array(
                'title'   => 'Option Name',
                'id'      => 'my_option_name',
                'type'    => 'text',
                'default' => '',
            ),
            array(
                'type' => 'sectionend',
                'id'   => 'my_settings_section',
            ),
        );
    }
}

add_filter( 'woocommerce_get_settings_pages', function( $settings ) {
    $settings[] = new My_Settings();
    return $settings;
} );
```

## HPOS feature compatibility declaration

Every WooCommerce extension MUST declare HPOS compatibility:

```php
add_action( 'before_woocommerce_init', function() {
    if ( class_exists( \Automattic\WooCommerce\Utilities\FeaturesUtil::class ) ) {
        \Automattic\WooCommerce\Utilities\FeaturesUtil::declare_compatibility(
            'custom_order_tables', __FILE__, true
        );
    }
} );
```
