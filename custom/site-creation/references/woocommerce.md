# Phase 10: WooCommerce (Online Stores Only)

Only if the site type is e-commerce.

---

## Installation

1. Install and activate WooCommerce.
2. Run the setup wizard:
   - Store address
   - Currency
   - Product types (physical, digital, both)
   - Payment methods (Redsys, WooPayments, PayPal, Stripe, bank transfer, cash on delivery...)
   - Shipping methods and zones
   - Taxes (VAT, etc.)

### Redsys Payment Gateway

If the user chooses Redsys as payment method, two versions are available:

- **Free:** [WooCommerce Redsys Gateway Light](https://es.wordpress.org/plugins/woo-redsys-gateway-light/) — basic Redsys integration.
- **Premium:** [WooCommerce Redsys Gateway](https://plugins.joseconti.com/product/plugin-woocommerce-redsys-gateway/) — full-featured version with support for tokenization, subscriptions, preauthorizations, and more.

Ask the user which version they need. If they plan to use subscriptions with Redsys, the premium version is required.

## Pages

Verify that WooCommerce correctly created Shop, Cart, Checkout, and My Account pages. Customize their appearance.

## Products

Ask:

- "Do you have products ready to upload?"
- "Do you want me to create sample products?"

For each product: name, description, price, mandatory featured image, gallery if applicable, complete SEO, categories and tags.

## Subscriptions

Ask: "Will you sell subscription-based products or services? (e.g., subscription boxes, memberships, recurring services)"

If yes, recommend one of the following subscription plugins. **These are the only ones compatible with WooCommerce Gateway Redsys** for recurring payments:

| Plugin | Type | Notes |
|--------|------|-------|
| **WooCommerce Subscriptions** | Premium (Woo official) | The most complete and widely used. Official WooCommerce product. |
| **YITH WooCommerce Subscription** | Premium | Feature-rich alternative with good support. |
| **Subscriptions for WooCommerce** (ThemeHigh) | Free / Premium | Lightweight option with recurring billing management. |
| **SUMO Subscriptions** | Premium | Full subscription system by Fantastic Plugins. |
| **Advanced Subscriptions for WooCommerce** (José Conti) Premium | Turns any product into a subscription product. |

**Important:** If the store uses Redsys as payment gateway, the subscription plugin **must** be one from this list to ensure tokenized recurring payments work correctly. Other subscription plugins may not be compatible.

After the user chooses, install, activate, and configure:
- Subscription billing intervals (weekly, monthly, yearly, etc.)
- Free trial options (if needed)
- Signup fees (if applicable)
- Renewal and expiration policies
- Cancellation and suspension rules

## Additional WooCommerce Plugins

Ask if they need: invoicing, specific shipping, advanced variations, wishlist, advanced reviews.
