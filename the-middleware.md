# A look at the Middleware

> Reading this section is **not required** in order to use this package. This is simply to give a deeper look into the packages internals.

The provided middleware takes care of resolving the url's hash to an actual `ShareableLink` instance just like regular [route model binding](https://laravel.com/docs/5.4/routing#route-model-binding) does. In addition, it also validates whether the link is active, expired or if the user has entered the correct password.

To register the midldeware add the following line to your `app/Http/Kernel.php` file.

```php
protected $routeMiddleware = [
    'shared' => \Sassnowski\LaravelShareableModel\Http\Middleware\ValidateShareableLink::class,
];
```

In your routes file you can now assign the middleware to your shared routes.

```php
// routes/web.php

Route::group(['middleware' => 'shared', function () {
    Route::get('/shared/articles/{shareable_link}', 'SharedArticlesController@show');
    Route::get('/shared/files/{shareable_link}', 'SharedFilesController@show');
});
```

If the user now visits `https://my-site.com/shared/files/egpZWPKbzmUB8aDz57ZXh58b8Jk` the `egpZWPKbzmUB8aDz57ZXh58b8Jk` will get resolved to the underlying `SharedLink` instance. Every shared link has a `shareable` property you can use to access the actual shared model.

## How it works

Each shared model gets assigned a unique `uuid` . This uuid is what you see in the resulting link. The `uuid` is then used to query the `shareable_links` table for the link instance.

The middleware performs a series of checks based on the link's configuration. For instance, it checks whether the link is expired, requires a password or is inactive.

