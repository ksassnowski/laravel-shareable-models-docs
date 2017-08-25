# Password protected routes

It's possible to password protect a shared link. To do so you simply set the password when building the link.

```php
ShareableLink::buildFor($model)->setPassword('super-secret-password');
```

If someone now visits the produced url they will get redirected to a password prompt

&lt;div style="text-align: center"&gt;

![](/assets/Screen Shot 2017-08-25 at 14.15.52.png)

&lt;/div&gt;

