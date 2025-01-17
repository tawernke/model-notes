# Create notes on eloquent models. Supports multiple note types as well as multi-tenancy

[![Latest Version on Packagist](https://img.shields.io/packagist/v/enginedigital/model-notes.svg?style=flat-square)](https://packagist.org/packages/enginedigital/model-notes)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/enginedigital/model-notes/run-tests?label=tests)](https://github.com/enginedigital/model-notes/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/enginedigital/model-notes/Check%20&%20fix%20styling?label=code%20style)](https://github.com/enginedigital/model-notes/actions?query=workflow%3A"Check+%26+fix+styling"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/enginedigital/model-notes.svg?style=flat-square)](https://packagist.org/packages/enginedigital/model-notes)

> Create notes on eloquent models. Supports multiple note types as well as multi-tenancy.

## Installation

You can install the package via composer:

```bash
composer require enginedigital/model-notes
```

You can publish and run the migrations with:

```bash
php artisan vendor:publish --provider="EngineDigital\Note\NoteServiceProvider" --tag="model-notes-migrations"
php artisan migrate
```

You can publish the config file with:
```bash
php artisan vendor:publish --provider="EngineDigital\Note\NoteServiceProvider" --tag="model-notes-config"
```

This is the contents of the published config file:

```php
return [
    'note_model' => EngineDigital\Note\Note::class,
    'note_default_type' => 'none',
    // key => 'formatter_class_with_invoke',
    // key => ['formatter', 'method'],
    'note_types' => [
        'none' => null, // dont touch formatted output
        'plain' => 'e', // escape in formatted output
        'html' => null, // dont touch formatted output
        'markdown' => [\Illuminate\Support\Str::class, 'markdown'],
        'json' => 'json_decode', // treat the note content as JSON
    ],
    'model_primary_key_attribute' => 'model_id',
    'encrypt_notes' => false,
    'tenant_model' => null, // App\Models\Company::class
    'tenant_resolver' => null, // a class that uses `__invoke` or a container function to get the id of the current tenant
    'author_model' => null, // App\Models\User::class
    'author_resolver' => null, // a class that uses `__invoke` or a container function to get the id of the current user
    'cache_time' => null, // cache time in seconds
    'load_with' => [], // which note relationships to eager load. Example: ['author', 'author.profile', 'author.roles'] or only specific columns ['author:id,name']
];
```

## Usage

```php
// User model uses EngineDigital\Note\HasNotes
$user->setNote('This is my cute little note!');
```

## Testing

```bash
composer run test
```

## Contributing

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for details.

## Credits

- [James Doyle](https://github.com/james2doyle)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
