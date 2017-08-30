# Configuring a Link

The `ShareableLinkBuilder` exposes a number of methods to configure the produced link to your liking.

## Active and inactive links

**Default: **`false`

```php
ShareableLink::buildFor($entity)->setActive();
```

Inactive links will redirect to a different route when visited. You can overwrite the redirect route in the config.

## Password protecting links

**Default: **`null`

```php
ShareableLink::buildFor($entity)->setPassword('super-secret');
```

When trying to visit a password protected link the user instead gets redirect to a password prompt. After entering the correct password the `uuid` of the link gets saved in the session. So no password is required on subsequent requests.

## Setting an expiration date

**Default:** `null`

```php
ShareableLink::buildFor($entity)->setExpirationDate();
```

Links with an expiration date will redirect the user to a different page after the link expired. The target url can be configured in the config.

## Setting a prefix

**Default:** `null`

```php
ShareableLink::buildFor($entity)->setPrefix('articles');
```

Defines a prefix for the generated route so you can target them more precisely in your routes file. By default all generated link take the form `/shared/{hash}`. If, for example, the prefix is set to `articles` the generated link would take the form of `/shared/articles/{hash}`. This is useful if you have different kinds of shareable models that should all get routed to different urls when visited.

## Notify on visit

**Default**: `false`

```php
ShareableLink::buildFor($entity)->notifyOnVisit();
```

When this option is set, a `LinkWasVisited` event gets thrown every time a user visits the link. You can access the visited link via the `$link` property on the event.

Note that the event only gets thrown if the visitor actually passes all checks that might have been configured on the link, e.g. password protection. So someone attempts to visit an expired link or enters a wrong password this event will not get thrown. 



