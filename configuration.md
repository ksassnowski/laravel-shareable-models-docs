# Configuring the package

To customize the package's config you first need to publish its assets. Run the following command in your terminal.

```bash
php artisan vendor:publish --provider="Sassnowski\LaravelShareableModel\ShareableLinkServiceProvider"
```

This will put a `shareable-model.php` in your `config` directory. In this file you can change the following options to fine-tune the package to your liking.

## Base Url

You can configure the base url by changing the `base_url` parameter.

| Option | What does it do? | Default |
| :--- | :--- | :--- |
| **base\_url** | Changes the base url of the generated link. By default the generated urls look like this: _/shared/{uuid}_. Changing this option to /foo would result in links looking like this: /foo/{uuid} | _**/shared**_ |

## Redirect Routes

This section specifies where the middleware will try to redirect if the link can not be accessed.

| Option | What does it do? | Default |
| :--- | :--- | :--- |
| **inactive** | Route the user will get redirected to if the visited link is inactive. | **/shared/inactive** |
| **expired** | Route the user will get redirected to if the visited link has expired. | **/shared/expired** |
| **password\_protected** | Route the user will get redirected to if the visited link is password protected and the user has not yet entered the correct password. | **/shared/password** |

**Note: **The `password_protected` is already implemented by the package. It is not recommended to change this route since this would require you to implement the route yourself. If you simply want to change the default view see [Password protected routes](/password-protected-routes.md#overriding).

