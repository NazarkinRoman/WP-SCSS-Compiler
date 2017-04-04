# WP SCSS Compiler
### <https://github.com/NazarkinRoman/WP-SCSS-Compiler/>

Simple class providing integration between WordPress and PHP SCSS Compiler by @leafo

## Usage
`WP-SCSS-Compiler` uses [leafo/scssphp](https://github.com/leafo/scssphp/) as a dependency so make sure to download it too. Once you have downloaded all necessary files, just require main file inside your `functions.php` file:

```
require_once 'WP_SCSS_Compiler.php';
```

And then equip your `scss` files just like regular `css` ones:
```
add_action( 'wp_enqueue_scripts', 'mytheme_enqueue_styles' );
function mytheme_enqueue_styles() {
	wp_enqueue_style( 'my-handlename', get_template_directory_uri() . '/styles-directory/file.scss' );
}

```

To pass variables into compiler use `wp_scss_variables` filter:
```
add_filter( 'wp_scss_variables', 'mytheme_scss_vars', 10, 2 );
function mytheme_scss_vars( $vars, $handle ) {

	if ( ! is_array( $vars ) ) {
		$vars = array();
	}

	// colors
	$vars['secondary-color'] = '#ccc';
	$vars['site-background'] = '#fff';

	// footer colors
	$vars['footer-text-color'] = get_theme_mod('footer_text_color');
	$vars['footer-bg-color']   = get_theme_mod('footer_bg_color');

	return $vars;
}
```

## Available filters and actions

- `wp_scss_import_dirs` filter. Can be used to modify import directories that will be passed to SCSS compiler
- `wp_scss_formatter` filter. Classname as a string of a formatter that should be used.
- `wp_scss_instance` action hook. Allows developers to mess around with the scss object configuration
- `wp_scss_cache_path` filter. Can be used to modify storage directory for compiled CSS files.
- `wp_scss_cache_url` filter. URL of a directory where compiled files are stored.