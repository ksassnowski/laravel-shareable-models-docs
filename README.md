# Laravel Shareable Models

This package allows you to generate shareable links from your Eloquent Models. **Think of it as dynamic routes that only exist for some models in your database.**

It takes something like this:

```php
class User extends Model {}
```

And turns it into this

```
https://my-sick-website.com/shared/egpZWPKbzmUB8aDz57ZXh58b8Jk
```

Now all you have to do is define a route

```php
Route::get('/shared/{shareable_link}', ['middleware' => 'shared', function (ShareableLink $link) {
    var_dump($link->shareable);
}]);

// object(User)#1 (0) {}
```

The hash in the url gets resolved automatically by the provided `shared` middleware. You can then accessed the shared model via the `shareable` property of the link. 

Here's a more complete example:

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



