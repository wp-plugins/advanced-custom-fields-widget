# ACF Widget

A widget that is able to use content from an ACF field group.

## Installation

* Download [the zip archive](https://github.com/alexvandervegt/advanced-custom-fields-widget/archive/master.zip)
* Put it in your wp-content/plugins folder
* Activate the plugin in your wp-admin

## Screenshots

##### ACF Widget Field group added

![ACF Widget Field group added](https://github.com/alexvandervegt/advanced-custom-fields-widget/raw/master/screenshot-1.png)

##### It has the option to select the desired ACF Field group

![It has the option to select the desired ACF Field group](https://github.com/alexvandervegt/advanced-custom-fields-widget/raw/master/screenshot-2.png)

##### After saving ACF Widget all fields are available (AJAX update is @TODO)

![After saving ACF Widget all fields are available](https://github.com/alexvandervegt/advanced-custom-fields-widget/raw/master/screenshot-3.png)

## Custom widgets

Are you a developer and want to make custom widgets with preset ACF Field groups, use the code snippet below.

#### Code snippet

PHP Class for a custom "Spotlight" widget (put it in your theme functions.php)

```php
class Spotlight_Widget extends ACF_Widget
{	
	function __construct()
	{
		$widget_options = array(
			"classname"     => "spotlight_widget", 
			"description"   => "Widget with image, title and a link."
			);

		parent::WP_Widget("Spotlight_Widget", "Spotlight", $widget_options);

		// Preset options for this widget
		$this->acf_group_id 	= 110;
		$this->title_field_key 	= "title";
	}

	function widget($args, $instance) 
	{
		// Variables
		$acf_key = "widget_" . $this->id_base . "_" . $this->number;

		// Widget HTML output
		include(realpath(dirname(__FILE__)) . "/../widgets/widget_spotlight.php");
	}
}

$GLOBALS["acf_widget_types"][] = "spotlight_widget";
register_widget("Spotlight_Widget");
```

In the HTML output of the widget we can access the ACF fields like this

```php
<?php the_field("title", $acf_key) ?>
```

#### Screenshot

![It's also possible to extend ACF Widget to make fully custom widgets for developers](https://github.com/alexvandervegt/advanced-custom-fields-widget/raw/master/screenshot-4.png)