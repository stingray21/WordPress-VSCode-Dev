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

### Install phpcs

**Add to path**

Add PATH to `.zshrc` or `.bash_profile` 
(check with `which phpcs`)
```
export PATH="$HOME/.config/composer/vendor/bin:$PATH"
```

[Ref](https://javorszky.co.uk/2018/07/30/set-up-phpcs-and-wordpress-extra-coding-standards-and-configure-your-ides-to-use-them/)

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
# https://make.wordpress.org/core/handbook/best-practices/coding-standards/

root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
indent_style = tab

[*.css]
indent_style = tab
indent_size = 4

[*.scss]
indent_style = tab
indent_size = 4

[*.txt]
end_of_line = crlf
```
[Source](https://github.com/WordPress/twentytwentyone/blob/trunk/.editorconfig) (alternatively [here](https://core.trac.wordpress.org/browser/trunk/.editorconfig) or [here](https://github.com/WordPress/wordpress-develop/blob/master/.editorconfig))


#### VS Code Plugins

- **EditorConfig for VS Code** by *EditorConfig*  
  [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) or  [Github](https://github.com/editorconfig/editorconfig-vscode)  
  Version:  	0.16.4 (2020-07-12)

## PHP CodeSniffer

[Github](https://github.com/squizlabs/PHP_CodeSniffer)

[Whitelisting code which flags errors](https://github.com/WordPress/WordPress-Coding-Standards/wiki/Whitelisting-code-which-flags-errors)

### Installation with Composer

```shell
composer global require "squizlabs/php_codesniffer=*"
```

Apparently PHPCS ([link to issue](https://github.com/squizlabs/PHP_CodeSniffer/issues/3182#issue-758524292)) nor WPCS ([link to issue](https://github.com/WordPress/WordPress-Coding-Standards/issues/1967#issue-770860444)) work at this point with PHP8 and won't until their next releases.

It's therefore recommended to use PHP 7.4 instead.
[WP StackExchange](https://wordpress.stackexchange.com/questions/385746/how-to-set-up-phpcs-with-wordpress-coding-standard-with-php8)

### "Hack" option

Instead of downgrading to PHP7, this seems to work. But it might cause any kinds of issues, so **use it at you own risk**.

Replacing the content of the local `ControlStructureSpacingSniff.php` file  
(*in `/WordPress/Sniffs/WhiteSpace/` of the cloned repo or the vendor folder of the composer installation*) with the [one](https://github.com/WordPress/WordPress-Coding-Standards/blob/7cd46bed1e6a7a2af3fe24c7f4a044da3076d8f4/WordPress/Sniffs/WhiteSpace/ControlStructureSpacingSniff.php) from the `develop` branch

### custom set of rules

https://github.com/WordPress/WordPress-Coding-Standards/blob/develop/phpcs.xml.dist.sample


### For Themes

```shell
composer global require --dev wptrt/wpthemereview
```

https://github.com/WPTT/WPThemeReview

### Troubleshooting

* Error: PHP 8 will throw and (uncaught) `TypeError: vsprintf(): Argument #2 ($args) must be of type array, string given`

	e.g.
	`phpcs: Uncaught TypeError: vsprintf(): Argument #2 ($values) must be of type array, string given in /home/XYZ/.config/composer/vendor/squizlabs/php_codesniffer/src/Files/File.php:1050`

	Problem with the WordPress sniff and not PHPCS  [Ref](https://github.com/squizlabs/PHP_CodeSniffer/issues/3196)

	Will (hopefully) be fixed soon ([see](https://github.com/WordPress/WordPress-Coding-Standards/commit/7cd46bed1e6a7a2af3fe24c7f4a044da3076d8f4))

* Conflicts with VSC Plugin [Format HTML in PHP](https://marketplace.visualstudio.com/items?itemName=rifi2k.format-html-in-php)



### Plugin for VS Code

[PHP Sniffer & Beautifier](https://marketplace.visualstudio.com/items?itemName=ValeryanM.vscode-phpsab) by *Samuel Hilson* 
  ([Github](https://github.com/valeryan/vscode-phpsab))  
  Version: 0.0.11 (2020-08-24)

Settings in `settings.json`
```json
	"[php]": {
    "editor.defaultFormatter": "valeryanm.vscode-phpsab"
	},
```
To make global installation of PHPCS and PHPCBF work:
```json
  "phpsab.executablePathCS": "/home/<USER>/.config/composer/vendor/bin/phpcs",
	"phpsab.executablePathCBF": "/home/<USER>/.config/composer/vendor/bin/phpcbf",
```
**replace `<USER>` with username*

This VS Code plugin works for me. There are other popular plugins, but either I could not get them to work or they have not been updated in a while.  
(see section: *Other VS Code Extensions*)


## ESLint with Prettier - Javascript

Doc: [eslint.org](https://eslint.org/docs/user-guide/getting-started)

Local Installation
```shell
npm install --save-dev eslint
```

Install rule set to extend [ESLint Plugin](https://www.npmjs.com/package/@wordpress/eslint-plugin)

```shell
npm install --save-dev @wordpress/eslint-plugin 
```

Example: [.eslintignore](https://github.com/WordPress/twentytwentyone/blob/trunk/.eslintignore) for TwentyTwentyOne Theme


Example: [.eslintrc](https://github.com/WordPress/twentytwentyone/blob/trunk/.eslintrc) for TwentyTwentyOne Theme

### Prettier (necessary?)

```shell
npm install --save-dev prettier eslint-plugin-prettier eslint-config-prettier 
```

### VS Code Extension

- [VS Code ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)  by *Dirk Baeumer* 
  ([Github](https://github.com/Microsoft/vscode-eslint))  
  Version: 	2.1.19 (2021-03-15)

Settings
```json
"eslint.alwaysShowStatus": true,
```

## Stylelint - CSS & Sass

https://stylelint.io/

[stylelint on npm](https://www.npmjs.com/package/stylelint) 

```shell
npm install --save-dev stylelint stylelint-scss
```


```shell
npm install --save-dev @wordpress/stylelint-config 
```

Add to `.stylelinrc`:
```json
{
	"extends": [
		"@wordpress/stylelint-config"
	],
	"rules": {
		
	}
}
```

For Sass: 
```json
{
	"extends": [
		"@wordpress/stylelint-config/scss"
	],
	"rules": {
		
	}
}
```
Example: [.stylelintrc](https://github.com/WordPress/twentytwentyone/blob/trunk/.stylelintrc.json) for TwentyTwentyOne Theme

`.stylelinignore`:
```json
vendor/
node_modules/
*.php
*.map
*.png
*.json
LICENSE
composer.lock
*.txt
```
Example: [.stylelintignore](https://github.com/WordPress/twentytwentyone/blob/trunk/.stylelintignore) for TwentyTwentyOne Theme


### VS Code Extension


- [stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint) by *stylelint* 
  ([Github](https://github.com/stylelint/vscode-stylelint))  
  Version: 0.86.0 (2021-02-07)

## Browserlist

[npm](https://www.npmjs.com/package/@wordpress/browserslist-config)

```shell
npm install --save-dev browserslist @wordpress/browserslist-config
```

Add this to `package.json`:

```json
"browserslist": [
	"extends @wordpress/browserslist-config"
]
```

Alternatively, use `.browserslistrc` file with:

```json
extends @wordpress/browserslist-config
```

## Other Tutorials

- [Setting Up PHP CodeSniffer in Visual Studio Code](https://tommcfarlin.com/php-codesniffer-in-visual-studio-code/) by Tom McFarlin (2020)

- [VS Code for WordPress Development](https://tommcfarlin.com/vs-code-wordpress/) by Tom McFarlin (2016)

- [Using PHP CodeSniffer For MAMP and WordPress](https://tommcfarlin.com/php-codesniffer/) by Tom McFarlin (2015)

- [Set Up PHP CodeSniffer for Local Development](https://www.twilio.com/blog/set-up-php-codesniffer-local-development-sublime-text-php-storm-vs-code) by  Michael Okoko (2020-01-10)

- [WordPress PHP CodeSniffer for your favorite editor](https://luminfire.com/2017/03/01/wordpress-php-codesniffer-favorite-editor/) by Marty Kokes, Michael Moore & Nick Ciske (2017-03-01)

- [Set up PHPCS and WordPress-Extra coding standards, and configure your IDEs to use them](https://javorszky.co.uk/2018/07/30/set-up-phpcs-and-wordpress-extra-coding-standards-and-configure-your-ides-to-use-them/) by Gabor Javorszky (2018-07-30) 


- [How to Install and Use Composer](https://www.hostinger.com/tutorials/how-to-install-composer) by Domantas G (2021-03-09)

## Other VS Code Extensions

- [PHP Essentials](https://marketplace.visualstudio.com/items?itemName=dudemelo.php-essentials)
  ([Github](https://github.com/dudemelo/vscode-php-essentials))  

- [WordPress Hooks IntelliSense](https://marketplace.visualstudio.com/items?itemName=johnbillion.vscode-wordpress-hooks) by *johnbillion* 
  ([Github](https://github.com/johnbillion/vscode-wordpress-hooks))  
  Version: 0.5.4 (2021-03-21)  

- [WPCS Whitelist Flags](https://marketplace.visualstudio.com/items?itemName=claudiosanches.wpcs-whitelist-flags) by *Claudio Sanches* 
  ([Github](https://github.com/claudiosanches/vscode-wpcs-whitelist-flags))  
  Version: 1.1.0 (2019-07-23)

- [PHP_CodeSniffer](https://marketplace.visualstudio.com/items?itemName=obliviousharmony.vscode-php-codesniffer) by *Christopher Allford* 
  ([Github](https://github.com/ObliviousHarmony/vscode-php-codesniffer))  
  Version: 1.1.0 (2021-03-05)

- [vscode-php-cs-fixer](https://marketplace.visualstudio.com/items?itemName=fterrag.vscode-php-cs-fixer) by *Frank Terragna* 
  ([Github](https://github.com/fterrag/vscode-php-cs-fixer))  
  Version:  0.4.0 (2020-08-23)

- [PHP Companion](https://marketplace.visualstudio.com/items?itemName=blanc-frederic.vs-phpcompanion) by *Fred Blanc* 
  ([Github](https://github.com/blanc-frederic/vs-phpcompanion))  
  Version: 2.1.0 (2021-03-11)

- [PHP Refactor](https://marketplace.visualstudio.com/items?itemName=tintrinh.php-refactor) by *Tin Trinh* 
  ([Github](https://github.com/htintrinh/php-refactor-vscode))  
  Version: 0.0.7 (2019-09-16)

- [phpcs](https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs&ssr=false#review-details) by *Ioannis Kappas* 
  ([Github](https://github.com/ikappas/vscode-phpcs))  
  Version: 1.0.5 (2018-03-01)

- [PHP Sniffer](https://marketplace.visualstudio.com/items?itemName=wongjn.php-sniffer&ssr=false#overview) by *wongjn* 
  ([Github](https://github.com/wongjn/vscode-php-sniffer))  
  Version: 1.3.0 (2020-11-14)
- [php cs fixer](https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer&ssr=false#overview)  by *junstyle* 
  ([Github](https://github.com/junstyle/vscode-php-cs-fixer))  
  Version: 	0.1.158 (2021-01-19)


## Other resources

### Developer Tools

- [WP Plugin Handbook - Developer Tools](https://developer.wordpress.org/plugins/developer-tools/)

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
