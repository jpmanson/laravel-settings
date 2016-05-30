# Persistent Settings Manager for Laravel

 * Simple key-value storage
 * Support multi-level array (dot delimited keys) structure.
 * Localization supported.

## Installation

1. install package

	```php
		composer require jpmanson/laravel-settings
	```

1. edit config/app.php

	service provider :

	```php
		Unisharp\Setting\SettingServiceProvider::class,
	```

    class aliases :

	```php
		'Setting' => Unisharp\Setting\SettingFacade::class,
	```

1. create settings table

	```php
		php artisan vendor:publish --tag=settings
		php artisan migrate
	```


## Usage

```php
	Setting::get('name', 'Computer');
	// get setting value with key 'name'
	// return 'Computer' if the key does not exists

	Setting::lang('zh-TW')->get('name', 'Computer');
	// get setting value with key and language

	Setting::set('name', 'Computer');
	// set setting value by key

	Setting::lang('zh-TW')->set('name', 'Computer');
	// set setting value by key and language

	Setting::has('name');
	// check the key exists, return boolean

	Setting::lang('zh-TW')->has('name');
	// check the key exists by language, return boolean

	Setting::forget('name');
	// delete the setting by key

	Setting::lang('zh-TW')->forget('name');
	// delete the setting by key and language
	
	Setting::get('name', 'Computer', true);
	// get setting value with key 'name'
	// return 'Computer' if the key does not exists and save the key in database
	// third parameter = true force to save the key with the provided default value if not exists
```

## Dealing with array

```php
	Setting::get('item');
	// return null;

	Setting::set('item', ['USB' => '8G', 'RAM' => '4G']);
	Setting::get('item');
	//  return array(
	//		  	'USB' => '8G',
	//	 		'RAM' => '4G'
	//  	);

	Setting::get('item.USB');
	// return '8G';
```
