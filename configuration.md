# Configuring the package

To customize the package's config you first need to publish its assets. Run the following command in your terminal.

```bash
php artisan vendor:publish --provider="Sassnowski\LaravelShareableModel\ShareableLinkServiceProvider"
```

This will put a `shareable-model.php` in your `config` directory. In this file you can change the following options to fine-tune the package to your liking.

## Redirect Routes

This section specifies where the middleware will try to redirect if the link can not be accessed.

| Option | What does it do? | Default |
| :--- | :--- | :--- |
| **inactive** | Route the user will get redirected to if the visited link is inactive. | **/shared/inactive** |
| **expired** | Route the user will get redirected to if the visited link has expired. | **/shared/expired** |
| **password\_protected** | Route the user will get redirected to if the visited link is password protected and the user has not yet entered the correct password. | **/shared/password** |

**Note: **The `password_protected` is already implemented by the package. It is not recommended to change this route since this would require you to implement the route yourself. If you simply want to change the default view see [Password protected routes](/password-protected-routes.md#overriding).

## Hashids

You can configure the underlying Hashid library to customize the generated hash.

| Option | What does it do? | Default |
| :--- | :--- | :--- |
| **min\_hash\_length** | The minimum length of the generated hash. Normally the length of the hash is dependent on the length of the input string. With this option you can enforce a minimum output length. | **10** |
| **salt** | The salt used to create the hashes. | **env\('APP\_KEY'\)** |
| **alphabet** | Specifies the allowed characters that can occur in the created hash. If you want to create hashes that are a bit more easy to remember you might want to remove ambiguous characters from the alphabet. | **abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890** |



