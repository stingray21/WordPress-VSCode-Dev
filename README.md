# WordPress VSCode Dev
Setting up VS Code for WordPress Theme and Plugin development



## Debugging 


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
[Source](https://github.com/WordPress/wordpress-develop/blob/master/.editorconfig)

or maybe [Source](https://core.trac.wordpress.org/browser/trunk/.editorconfig)?


## Troubleshooting


