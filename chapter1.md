# Installation

## Requirements

* PHP &gt;= 7.0
* Laravel &gt;= 5.4

## Installing the package

Require the package through composer

```
composer require sassnowski/laravel-shareable-models
```

Then add the service provider to your `config/app.php`.

```php
// app/config.php

'providers' => [
    Sassnowski\LaravelShareableModel\ShareableLinkServiceProvider::class,    
],
```

That's it for the basic setup. Let's move on to the interesting part!

