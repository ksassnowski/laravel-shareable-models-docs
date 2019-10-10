# Introduction

This package allows you to generate shareable links from your Eloquent Models. **Think of it as dynamic routes that only exist for some models in your database.**

It takes something like this:

```php
class User extends Model {}
```

And turns it into this

```text
https://my-sick-website.com/shared/0004c748a2a14b9293a73d0051840805
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
use Sassnowski\LaravelShareableModel\Shareable\ShareableLink;

// Assume we have a user record for which we want to generate 
// a shareable link 
$user = User::create([
    'name' => 'Kai Sassnowski',
    'email' => 'me@kai-sassnowski.com',
    'password' => bcrypt('super-secret'), // please don't hack me
]);

$link = ShareableLink::buildFor($user)
    // We can password protect the created link.
    ->setPassword('hunter2')

    // By default generated links are inactive.
    ->setActive()

    // You can prefix the created link to create unique routes
    // for different models. For example this would create a 
    // url like `/shared/users/{uuid}`.
    ->setPrefix('users')

    // We can configure the link to throw an event every time
    // it is visited by a user. That way you can attach arbitrary
    // event listeners to it. For example, you might want to
    // notify the user who shared the link via email that it has
    // been visited.
    ->notifyOnVisit()

    // We can assign an expiration date to a link to ensure
    // it can only be visited until a certain date.
    ->setExpirationDate(Carbon::now()->addDay())

    // Finally, when you have configured the link to your liking
    // all that is left to do is to actually create it. This will
    // save the created link to the database and return the instance.
    ->build();

var_dump($link->url);

// string(57) "http://localhost/shared/users/0004c748a2a14b9293a73d0051840805"
```

