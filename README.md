# WordPress VSCode Dev
Setting up VS Code for WordPress Theme and Plugin development


**Status**  
Date: *March 2021*  
VS Code: *v1.54.3*  
PHP: *v8.0.3*  
WP: *5.7*  



## Debugging 

### WP Debugging settings

[WP Codex](https://codex.wordpress.org/WP_DEBUG)

in `wp-config.php`:
```php
// Enable debugging
define( 'WP_DEBUG', true ); 
// errors saved to a debug.log log file inside the /wp-content/ directory
define( 'WP_DEBUG_LOG', true ); 
//controls whether debug messages are shown inside the HTML of pages 
define( 'WP_DEBUG_DISPLAY', true ); 
```

### PHP - xDebug


### JS




## Coding Standard 


[WordPress Coding Standards](https://developer.wordpress.org/coding-standards/)

WordPress Coding Standards for PHP_CodeSniffer  
[Github: WordPress-Coding-Standards](https://github.com/WordPress/WordPress-Coding-Standards/)

**Deprecated**  
[@WordPress-Coding-Standards/stylelint-config-wordpress
](https://github.com/WordPress-Coding-Standards/stylelint-config-wordpress)





### Editor config

[EditorConfig](https://editorconfig.org/)


`.editorconfig`:

```
# This file is for unifying the coding style for different editors and IDEs
# editorconfig.org

# WordPress Coding Standards
# https://make.wordpress.org/core/handbook/coding-standards/

root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
indent_style = tab

[*.yml]
indent_style = space
indent_size = 2

[*.md]
trim_trailing_whitespace = false

[{*.txt,wp-config-sample.php}]
end_of_line = crlf
```
[Source](https://github.com/WordPress/wordpress-develop/blob/master/.editorconfig) (or maybe [here](https://core.trac.wordpress.org/browser/trunk/.editorconfig))


### PHP CodeSniffer

[Github](https://github.com/squizlabs/PHP_CodeSniffer)

#### Installation with Composer

```shell
composer global require "squizlabs/php_codesniffer=*"
```

#### Troubleshooting

* Error: PHP 8 will throw and (uncaught) `TypeError: vsprintf(): Argument #2 ($args) must be of type array, string given`

	e.g.
	`phpcs: Uncaught TypeError: vsprintf(): Argument #2 ($values) must be of type array, string given in /home/XYZ/.config/composer/vendor/squizlabs/php_codesniffer/src/Files/File.php:1050`

	Problem with the WordPress sniff and not PHPCS  [Ref](https://github.com/squizlabs/PHP_CodeSniffer/issues/3196)

	Will (hopefully) be fixed soon ([see](https://github.com/WordPress/WordPress-Coding-Standards/commit/7cd46bed1e6a7a2af3fe24c7f4a044da3076d8f4))
