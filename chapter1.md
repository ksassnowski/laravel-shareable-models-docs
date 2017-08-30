# Installation

## Requirements

* `PHP >= 7.0`
* `Laravel >= 5.4`

## Installing the package

Require the package through composer

```
$ composer require sassnowski/laravel-shareable-models
```

### Register the Service Provider \(Laravel &lt;= 5.4\)

Laravel 5.5 introduced auto discovery support. If you are still on 5.4 add the service provider to your `config/app.php`.

```php
// app/config.php

'providers' => [
    Sassnowski\LaravelShareableModel\ShareableLinkServiceProvider::class,
],
```

Run the provided migration to create the `shareable_links` table.

```
$ php artisan migrate

Migrating: 2017_05_21_232515_create_shareable_links_table
Migrated:  2017_05_21_232515_create_shareable_links_table
```

## Register the middleware

Add the following line to the `$routeMiddleware` array in your `app/Http/Kernel.php`to register the middleware that comes with this package.

```php
protected $routeMiddleware = [
    'shared' => \Sassnowski\LaravelShareableModel\Http\Middleware\ValidateShareableLink::class,
];
```

## \(Optional\) Publish assets

If you want, you can publish the packages assets by running the following command.

```
php artisan vendor:publish --provider="Sassnowski\LaravelShareableModel\ShareableLinkServiceProvider"
```

That's it for the basic setup. Let's move on to the interesting part!

