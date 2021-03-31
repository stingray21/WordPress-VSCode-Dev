# WordPress VSCode Dev
Setting up VS Code for WordPress Theme and Plugin development


**Status**  
Date: *March 2021*  
VS Code: *v1.54.3*  
PHP: *v8.0.3* ([Versions](https://www.php.net/supported-versions.php))  
WP: *5.7* ([Releases](https://wordpress.org/download/releases/))



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


#### VS Code Plugins

- **PHP Debug** by *Felix Becker*  
  [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug) or  [Github](https://github.com/xdebug/vscode-php-debug)  
  Version: 1.14.12 (2021-03-27)
  


### JS




## Coding Standard 


[WordPress Coding Standards](https://developer.wordpress.org/coding-standards/)

WordPress Coding Standards for PHP_CodeSniffer  
[Github: WordPress-Coding-Standards](https://github.com/WordPress/WordPress-Coding-Standards/)

**Deprecated**  
[@WordPress-Coding-Standards/stylelint-config-wordpress
](https://github.com/WordPress-Coding-Standards/stylelint-config-wordpress)

**Installation with composer**
```shell
composer global require wp-coding-standards/wpcs
```

## PHP_CodeSniffer Standards Composer Installer Plugin

For easy installation of PHPCS coding standards (The plugin will configure the `installed_paths` option.).

[Github](https://github.com/DealerDirect/phpcodesniffer-composer-installer)

```shell
composer global require dealerdirect/phpcodesniffer-composer-installer
```


## Editor config

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


#### VS Code Plugins

- **EditorConfig for VS Code** by *EditorConfig*  
  [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) or  [Github](https://github.com/editorconfig/editorconfig-vscode)  
  Version:  	0.16.4 (2020-07-12)

## PHP CodeSniffer

[Github](https://github.com/squizlabs/PHP_CodeSniffer)

### Installation with Composer

```shell
composer global require "squizlabs/php_codesniffer=*"
```

Apparently PHPCS ([link to issue](https://github.com/squizlabs/PHP_CodeSniffer/issues/3182#issue-758524292)) nor WPCS ([link to issue](https://github.com/WordPress/WordPress-Coding-Standards/issues/1967#issue-770860444)) work at this point with PHP8 and won't until their next releases.

It's therefore recommended to use PHP 7.4 instead.
[WP StackExchange](https://wordpress.stackexchange.com/questions/385746/how-to-set-up-phpcs-with-wordpress-coding-standard-with-php8)

#### "Hack" option

Instead of downgrading to PHP7, this seems to work. But it might cause any kinds of issues, so **use it at you own risk**.

Replacing the content of the local `ControlStructureSpacingSniff.php` file  
(*in `/WordPress/Sniffs/WhiteSpace/` of the cloned repo or the vendor folder of the composer installation*) with the [one](https://raw.githubusercontent.com/WordPress/WordPress-Coding-Standards/develop/WordPress/Sniffs/WhiteSpace/ControlStructureSpacingSniff.php) from the `develop` branch



#### Troubleshooting

* Error: PHP 8 will throw and (uncaught) `TypeError: vsprintf(): Argument #2 ($args) must be of type array, string given`

	e.g.
	`phpcs: Uncaught TypeError: vsprintf(): Argument #2 ($values) must be of type array, string given in /home/XYZ/.config/composer/vendor/squizlabs/php_codesniffer/src/Files/File.php:1050`

	Problem with the WordPress sniff and not PHPCS  [Ref](https://github.com/squizlabs/PHP_CodeSniffer/issues/3196)

	Will (hopefully) be fixed soon ([see](https://github.com/WordPress/WordPress-Coding-Standards/commit/7cd46bed1e6a7a2af3fe24c7f4a044da3076d8f4))


### Plugin for VS Code

**PHP Sniffer** by *wongjn *
Version: 1.3.0 (2020-11-14)

[VS Marketplace](https://marketplace.visualstudio.com/items?itemName=wongjn.php-sniffer&ssr=false#overview)
[Github](https://github.com/wongjn/vscode-php-sniffer)

Settings in `settings.json`
```json
{
	"phpSniffer.standard": "WordPress",
	"[php]": {
		"editor.defaultFormatter": "wongjn.php-sniffer"
	}
}
```

This plugin works for me without many issues.
There are other popular plugins, but either I could not get them to work or they have not been updated in a while.

- **phpcs** by *Ioannis Kappas*  
  [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs&ssr=false#review-details) or   [Github](https://github.com/ikappas/vscode-phpcs)  
  Version: 1.0.5 (2018-03-01)
- **PHP Sniffer & Beautifier** by *Samuel Hilson*
  [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=ValeryanM.vscode-phpsab)
  [Github](https://github.com/valeryan/vscode-phpsab)
  Version: 0.0.11 (2020-08-24)
- **php cs fixer** by *junstyle*  
  [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer&ssr=false#overview) or [Github](https://github.com/junstyle/vscode-php-cs-fixer)  
  Version: 	0.1.158 (2021-01-19)

## Other Tutorials

- [Setting Up PHP CodeSniffer in Visual Studio Code](https://tommcfarlin.com/php-codesniffer-in-visual-studio-code/) by Tom McFarlin (2020)

- [VS Code for WordPress Development](https://tommcfarlin.com/vs-code-wordpress/) by Tom McFarlin (2016)

- [Using PHP CodeSniffer For MAMP and WordPress](https://tommcfarlin.com/php-codesniffer/) by Tom McFarlin (2015)

- [Set Up PHP CodeSniffer for Local Development](https://www.twilio.com/blog/set-up-php-codesniffer-local-development-sublime-text-php-storm-vs-code) by  Michael Okoko (2020-01-10)

- [WordPress PHP CodeSniffer for your favorite editor](https://luminfire.com/2017/03/01/wordpress-php-codesniffer-favorite-editor/) by Marty Kokes, Michael Moore & Nick Ciske (2017-03-01)

- [Set up PHPCS and WordPress-Extra coding standards, and configure your IDEs to use them](https://javorszky.co.uk/2018/07/30/set-up-phpcs-and-wordpress-extra-coding-standards-and-configure-your-ides-to-use-them/) by Gabor Javorszky (2018-07-30) 


- [How to Install and Use Composer](https://www.hostinger.com/tutorials/how-to-install-composer) by Domantas G (2021-03-09)

## VS Code Extensions

- [PHP Essentials](https://marketplace.visualstudio.com/items?itemName=dudemelo.php-essentials)  
  (on [Github](https://github.com/dudemelo/vscode-php-essentials))

- [PHP Sniffer](https://marketplace.visualstudio.com/items?itemName=wongjn.php-sniffer)  
  (on [Github](https://github.com/wongjn/vscode-php-sniffer))



## Other resources

### Boilerplate - Plugins
- WordPress Plugin Boilerplate [wppb.io](https://wppb.io/)  
  (on [Github](https://github.com/DevinVinson/WordPress-Plugin-Boilerplate))

### Boilerplate - Themes
- https://underscores.me/  
  (on [Github](https://github.com/automattic/_s))
- https://barebones.dev/get-started/  
  (on [Github](https://github.com/benchmarkstudios/barebones))
- http://tidythemes.com/  
  https://wordpress.org/themes/blankslate/  
  (on [Github](https://github.com/tidythemes/blankslate))
