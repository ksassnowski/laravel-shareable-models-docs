# Installation

## Requirements

* PHP &gt;= 7.0
* Laravel &gt;= 5.4

## Installing the package

Require the package through composer

```
$ composer require sassnowski/laravel-shareable-models
```

Then add the service provider to your `config/app.php`.

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

## \(Optional\) Publish assets

If you want, you can publish the packages assets by running the following command.

```
php artisan vendor:publish --provider="Sassnowski\LaravelShareableModel\ShareableLinkServiceProvider"
```

That's it for the basic setup. Let's move on to the interesting part!

