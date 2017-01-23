# WooCommerce

##Remove WooCommerce SKUs Completely

If you don’t need to use SKUs at all in your shop, you can disable them completely by using this code snippet in your custom site plugin. or theme’s functions.php:

```
add_filter( 'wc_product_sku_enabled', '__return_false' );
```

##Remove WooCommerce SKUs Only on Product Pages

To disable SKUs completely on product pages, but leave them for use in the admin for administration purposes, use the following snippet.

```
add_filter( 'wc_product_sku_enabled', function ( $enabled ) {
    if ( ! is_admin() && is_product() ) {
        return false;
    }
    return $enabled;
});
```
##Remove Product Tabs

To remove one or more product tabs unset the desired array key.

```
add_filter( 'woocommerce_product_tabs', function($tabs){
	unset($tabs['description']);     			// Remove Description tab
	unset($tabs['additional_information']);  	// Remove Additional Information tab
	unset($tabs['reviews']); 					// Remove Reviews tab

	return $tabs;
}, 100 );
```
##Remove one or more product categories from WooCommerce shop page

```
function remove_cat_from_shop_loop($q) {

	if (!$q->is_main_query()) {
		return;
	}

	if (!$q->is_post_type_archive()) {
		return;
	}

	if (!is_admin() && is_shop()) {
		$q->set('tax_query', [[
			'taxonomy' => 'product_cat',
			'field'    => 'slug',
			'terms'    => ['cat-1', 'cat-2'], // Change it to the slug/s you want to hide
			'operator' => 'NOT IN',
		]]);
	}

	remove_action('pre_get_posts', 'remove_cat_from_shop_loop');
}

add_action('pre_get_posts', 'remove_cat_from_shop_loop');
```

##Remove one or more category from the WooCommerce category widget

### Category List
```
add_filter('woocommerce_product_categories_widget_args', function ($args) {
	$args['exclude'] = [1,2,3];
	return $args;
});
```
### Category Dropdown
```
add_filter('wc_product_dropdown_categories_get_terms_args', function ($args) {
	$args['exclude'] = [1,2,3];
	return $args;
});
```
