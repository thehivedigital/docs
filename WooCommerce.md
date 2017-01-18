# Woocommerce

##Remove WooCommerce SKUs Completely

If you don’t need to use SKUs at all in your shop, you can disable them completely by using this code snippet in your custom site plugin or theme’s functions.php:

`
add_filter( 'wc_product_sku_enabled', '__return_false' );
`

##Remove WooCommerce SKUs Only on Product Pages

To disable SKUs completely on product pages, but leave them for use in the admin for administration purposes, use the following snippet.

`
add_filter( 'wc_product_sku_enabled', '__return_false' );
add_filter( 'wc_product_sku_enabled', '__return_false' );
`
