# Getting Started

## Preparing your Model

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



