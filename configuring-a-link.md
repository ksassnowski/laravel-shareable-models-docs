# Configuring a Link

_Coming soon_

## Active and inactive links

```php
<?php

ShareableLink::buildFor($entity)->setActive();
```

## Password protecting links

```php
<?php

ShareableLink::buildFor($entity)->setPassword('super-secret');
```

## Setting an expiration date

```php
<?php

ShareableLink::buildFor($entity)->setExpirationDate();
```

## Setting a prefix

```php
<?php

ShareableLink::buildFor($entity)->setPrefix('articles');
```



