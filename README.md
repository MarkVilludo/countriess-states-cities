# countries-states-cities
Laravel package for addresses that mostly used for dropdown in form.

## Installation

1. Require this package with composer.

```shell

composer require mark-villudo/countries-states-cities

```

2. Now add the service provider in config/app.php file:

```
'providers' => [
    // ...
    MarkVilludo\CountryStateCities\ServiceProvider::class,
];
```
3. Publish Seeder and Migration files

You can publish the migration with:

```

php artisan vendor:publish --provider="MarkVilludo\CountryStateCities\ServiceProvider" --tag="migrations"

```

Then, run
```

php artisan migrate

```

You can publish the seeder with:

```

php artisan vendor:publish --provider="MarkVilludo\CountryStateCities\ServiceProvider" --tag="seeder"

```

Declare published seeder in DatabaseSeeder.php

```
public function run()
{
  $this->call(CountryTableSeeder::class);
  $this->call(ProvincesTableSeeder::class);
  $this->call(CitiesTableSeeder::class);
}
```

Then, run
```

php artisan db:seed

```

You can publish its default controllers

```

php artisan vendor:publish --provider="MarkVilludo\CountryStateCities\ServiceProvider" --tag="controllers"

```

4. Make resource file for models. for Countries, Provinces, and Cities.

```
php artisan make:resource CountryResource
php artisan make:resource ProvinceResource
php artisan make:resource CityResource
```

```
php artisan make:model Models/Country
php artisan make:model Models/Province
php artisan make:model Models/City
```

5. Add this route in routes/api.php
```

Route::prefix('v1')->group(function () {
  //Country, Province/State and City
  Route::prefix('countries')->group(function () {
    Route::get('/','Api\CountryController@index');
    Route::get('/{id}/provinces','Api\ProvinceController@index');
  });
  Route::prefix('provinces')->group(function () {
    Route::get('/{id}/cities','Api\CityController@index');
  });
});

```

## Usage

//Serve app. `php artisan serve`

//Access the url from the code added in routes/api.php
```
http://127.0.0.1:8000/api/v1/countries
http://127.0.0.1:8000/api/v1/countries/169/provinces
http://127.0.0.1:8000/api/v1/provinces/46/cities
```

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
