# Membership

## Support matrix

| Laravel | PHP |
| --- | --- |
| 12.x | 8.3–8.5 |
| 13.x | 8.3–8.5 |

This release (version 2.0.0 and above) targets Laravel 12 and 13. It requires PHP 8.3 or newer. For Laravel 10 and below, refer to version 1.x.x.

## Instalation 
### Install Package Via Composer
```
composer require timedoor/tmd-membership
```

Install Membership
```
php artisan membership:install
```
Publish config & migration
```
php artisan vendor:publish --tag=tmd-membership
```
>  this will copy config `tmd-membership` and migration files


After that you can run 
```
php artisan migrate
```

After migration complete you have to add this section to `composer.json`
```json
"files": [
        "app/Helpers/membership.php"
    ]
```
 you can see detail of code here
```json
    "autoload-dev": {
            "psr-4": {
                "Tests\\": "tests/"
            },
            "files": [
                "app/Helpers/membership.php"
            ]
        },
```

Reload autoload
```
composer dump-autoload
```

### Register routes (Laravel 12+)

Laravel 12+ does not use `RouteServiceProvider` by default. Add the package routes in `bootstrap/app.php` using the `then` callback:

```php
use Illuminate\Support\Facades\Route;

return Application::configure(basePath: dirname(__DIR__))
    // ...
    ->withRouting(
        web: __DIR__.'/../routes/web.php',
        api: __DIR__.'/../routes/api.php',
        commands: __DIR__.'/../routes/console.php',
        health: '/up',
        then: function () {
            Route::middleware('api')
                ->prefix('api/v1')
                ->group(base_path('routes/membership.php'));

            Route::middleware('web')
                ->prefix('admin')
                ->name('admin.')
                ->group(base_path('routes/admin.php'));
        },
    )
    // ...
    ->create();
```

The package route files already define the `/api` and `/admin` prefixes. Do not add those prefixes again.

> Laravel 11 and earlier: register the same route groups in `app/Providers/RouteServiceProvider.php`.

Add Fcm trait to your user models
```php
Timedoor\TmdMembership\traits\Fcmable;

use Fcmable;
```

>## Membership Ready To Use
<br />

## Admin Url
```
{{url}}/admin/dashboard
```
## API Url
| Module | Url | Method |
| --- | --- | --- |
| Register | `{{url}}/register` | GET |
| Login | `{{url}}/login` | GET |
| Profile | `{{url}}/user` | GET |
| OTP | --- | --- |
| Request | `{{url}}/otp/request` | POST |
| Check | `{{url}}/otp/check` | POST |

## You can get current FCM token
```php
$request->user()->currentFcmToken()->token
```
<br />

### CRM Docs
https://band-othnielia-951.notion.site/Fcm-Package-431e6af9f4994da0bebff360c702c04e
<br />
<br />


# Thank You
