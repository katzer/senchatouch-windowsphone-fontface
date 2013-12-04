senchatouch-windowsphone-fontface
=================================

Windows Phone does not allow to specify @font-faces if the page was loaded via file: protocol, e.g if the page is hosted locally on the phone itself.

Since [Sencha Touch](http://www.sencha.com/forum/showthread.php?261159-ST2.2RC-WP8-Cordova-icon-font-not-shown) uses @font-faces to display icons, only the content letter will be visible on Windows Phone.

As the only workaround all icons has to be loaded as background images instead.

## Sass configuration
#### 1. Exclude pictos font and default icons
```scss
$include-pictos-font: false;
$include-default-icons: false;
```
#### 2. Import the variables for windows
```scss
@import "sencha-touch/windows";
@import "sencha-touch/default";
```
#### 3. Import the WindowsPhoneIcon.scss mixin
```scss
@import "stylesheets/mixins/windowsphone-icon";
```
#### 4. Import the icons you need
```scss
@import windowsphone-icon("home", "icons/home.png");
@import windowsphone-icon("star", "icons/star.png", "icons/star_active.png");
```

## Sass mixin
```scss
@mixin windowsphone-icon($name, $icon, $active-icon: null) {
	.x-tab .x-button-icon.#{$name}:before,
	.x-button .x-button-icon.#{$name}:before {
		content: none;
	}

	.x-tab .x-button-icon.#{$name} {
		background-size: 65%;
		background-position: 6px 6px;
	}

	.x-button-icon.#{$name} {
		background-image: theme_image("../../../../resources/", #{$icon});
		background-repeat: no-repeat;
		background-size: contain;
	}

	@if $active-icon != null {
		.x-tab-active .x-button-icon.#{$name},
		.x-tab-pressed .x-button-icon.#{$name},
		.x-button-pressing .x-button-icon.#{$name} {
			background-image: theme_image("../../../../resources/", #{$active-icon});
		}
	}
}
```

## License

This source code is released under the [MIT License](http://opensource.org/licenses/MIT).
