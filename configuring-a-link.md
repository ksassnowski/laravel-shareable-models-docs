# Configuring a Link

The `ShareableLinkBuilder` exposing a number of methods to configure the produced link to your liking.

## Active and inactive links

```php
ShareableLink::buildFor($entity)->setActive();
```

## Password protecting links

```php
ShareableLink::buildFor($entity)->setPassword('super-secret');
```

## Setting an expiration date

```php
ShareableLink::buildFor($entity)->setExpirationDate();
```

## Setting a prefix

```php
ShareableLink::buildFor($entity)->setPrefix('articles');
```



