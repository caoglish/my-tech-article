## Laravel Collection Macro
<!-- Language-All: php -->

### Extend collection method by using a macro

The `macro()` function allows you to add new functionality to `Illuminate\Support\Collection` objects

Usage:

```php
    Collection::macro("macro_name", function ($parameters) {
        // Your macro
    });
```

For example:

```php
    Collection::macro('uppercase', function () {
        return $this->map(function ($item) {
            return strtoupper($item);
        });
    });

    collect(["hello", "world"])->uppercase();
```

Result: `["HELLO", "WORLD"]`

### use Service Provider to register all macro
Collection macro must be loaded before using them. You should write marco in the provider. One way is that you can write macro in existed provider called AppServiceProvider or you can make your own provider. The Artisan CLI can generate a new provider by:

```cli
    php artisan make:provider CollectionMacroServiceProvider
```

in CollectionMacroServiceProvider file, put macro code in boot() method.

```php
    <?php
    namespace App\Providers;

    use Illuminate\Support\Collection;
    use Illuminate\Support\ServiceProvider;

    class CollectionMacroServiceProvider extends ServiceProvider
    {
        public function boot()
        {
        //marco code here
        }
        public function register()
        {
        }
    }
```

register the provider in `config/app.php`

```php
//in config/app.php file
 'providers' => [
  //  ...,
     App\Providers\CollectionMacroServiceProvider::class,
]

```

After setup the service provider, you cans use the extended methods  anywhere in your project.