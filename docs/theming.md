# Theming the Full Calendar jQuery Plugin

The Full Calendar jQuery plugin is themable using [jQuery UI ThemeRoller](http://jqueryui.com/themeroller/).

*Included Themes:* flick, redmond

## Adding Themes

Customize and download your theme from [jQuery UI ThemeRoller](http://jqueryui.com/themeroller/) and zip the folder located within the **css** folder (this folder should contain two CSS files and an images folder). Upload the zip file into `/_files/css/vendor/jqueryui` using the Zip Archive tool.

## Changing Themes

Modify the block located at `/_cascade/blocks/calendar head files`. Update the CSS `<link href="/_files/css/vendor/jqueryui/{THEME_NAME}/theme.min.css" rel="stylesheet" type="text/css"/>` tag to point to the compressed (minimized) CSS file of the desired theme.

**Note:** It is recommended to publish the theme folder located at `/_files/css/vendor/jqueryui` before publishing the Full Calendar to ensure the styles and images are available.