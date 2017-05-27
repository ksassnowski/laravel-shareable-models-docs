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
public function ShareableLink::buildFor(ShareableInterface $entity): ShareableLinkBuilder;
```

As you can see, this method returns an instance of `ShareableLinkBuilder`. This class allows you to configure the link to your liking. When you are done configuring simply call the `build()` method on the builder to create the actual link.

```php
$article = Article::find(1);

$link = ShareableLink::buildFor($article)
    ->setActive()
    ->build();
    
var_dump($link);
```



