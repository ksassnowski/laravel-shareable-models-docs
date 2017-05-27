# Laravel Shareable Models

This package allows you to generate shareable links from your Eloquent Models.

```php
<?php

use Carbon\Carbon;
use Sassnowski\LaravelShareableModel\ShareableLink;

// Assume we have a user record for which we want to generate 
// a shareable link 
$user = User::create([
    'name' => 'Kai Sassnowski',
    'email' => 'me@kai-sassnowski.com',
    'password' => bcrypt('super-secret'),
]);

$link = ShareableLink::buildFor($user)
    // We can password protect the created link
    ->setPassword('hunter2')
    
    // By default generated links are inactive
    ->setActive()
    
    // You can prefix the created link to create unique routes
    // for different models
    ->setPrefix('users')
    
    // We can assign an expiration date to a link to ensure
    // it can only be visited until a certain date.
    ->setExpirationDate(Carbon::now()->addDay())
    ->build();

var_dump($link->url);

// string(57) "http://localhost/shared/users/egpZWPKbzmUB8aDz57ZXh58b8Jk"
```

Think of it as dynamic routes, that only exist for certain models.

