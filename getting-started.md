# Getting Started

## Preparing your Model

In order for your model to be shareable it needs to implement `ShareableInterface`. This package comes with a default implementation that you can use by including the provided `Shareable` trait.

```php
<?php

use Illuminate\Eloquent\Model;
use Sassnowski\LaravelShareableModel\Shareable\Shareable;
use Sassnowski\LaravelShareableModel\Shareable\ShareableInterface;

class Article extends Model implements ShareableInterface
{
    use Shareable;    
}
```

## Building a shareable link

In order to create a shareable link for a particular `Article` you can utilise the `ShareableLink::buildFor()` factory method.

```php
public static function ShareableLink::buildFor(ShareableInterface $entity): ShareableLinkBuilder;
```

As you can see, this method returns an instance of `ShareableLinkBuilder`. This class allows you to configure the link to your liking. When you are done configuring simply call the `build()` method on the builder to create the actual link.

```php
<?php

$article = Article::find(1);

$link = ShareableLink::buildFor($article)
    ->setActive()
    ->build();
```

By calling `build()` you actually create the shareable link and save it to the database. Behind the scenes it is using Laravel's [Polymorphic Relationships](https://laravel.com/docs/5.4/eloquent-relationships#polymorphic-relations) to associate this link with the model you passed to the `buildFor` model.

### Getting the shared model from the link

If you used the provided `Shareable`trait you can retrieve the shared model by accessing the `shareable` property on the link.

```php
<?php

$article = $link->shareable;

// $article is now the model we shared in the above example.
```

## Creating a route

Now that we have a link what can we do with it? Until now our application does not even know how to respond to that url. So lets create a new route.

```php
<?php

// web.php

Route::get('shared/{shareable_link}', ['middleware' => 'shared', function (ShareableLink $link) {
    return $link->shareable;
});
```

**Note that we are applying the `shared` middleware to our route. This is required for the route model binding to work.**

Now if we try to access the generated link we should see the JSON serialized `Article` we shared earlier.

```php
<?php

var_dump($link->url);
// http://localhost:8000/shared/2E02L5m2rxibV8j4M3Aksyep0LE
```

```
$ curl http://localhost:8000/shared/4aQQLDa525h8NVPGxLZ4hqx0l46

{"id":1,"title":"The Raven","contents":"Once upon a midnight dreary, while I pondered, weak and weary...","created_at":"2017-05-31 19:35:28","updated_at":"2017-05-31 19:35:28"}
```

And that's the basic workflow. At this point, you can treat it like any other route in your application. You have absolute freedom to do whatever you want with this shared resource. Think of it as a regular `show` route **but instead of being defined for every model it is only defined for the ones you shared first**. This gives you an incredible amount of flexibility.

