# Laravel Transactional Model Events

[![Latest Version on Packagist](https://img.shields.io/packagist/v/mvanduijker/laravel-transactional-model-events.svg?style=flat-square)](https://packagist.org/packages/mvanduijker/laravel-transactional-model-events)
[![Build Status](https://img.shields.io/travis/mvanduijker/laravel-transactional-model-events/master.svg?style=flat-square)](https://travis-ci.org/mvanduijker/laravel-transactional-model-events)
[![Quality Score](https://img.shields.io/scrutinizer/g/mvanduijker/laravel-transactional-model-events.svg?style=flat-square)](https://scrutinizer-ci.com/g/mvanduijker/laravel-transactional-model-events)
[![Total Downloads](https://img.shields.io/packagist/dt/mvanduijker/laravel-transactional-model-events.svg?style=flat-square)](https://packagist.org/packages/mvanduijker/laravel-transactional-model-events)


Add transactional events to your eloquent models. Will automatically detect changes in your models within a transaction 
and will fire events on commit or rollback. Should mimic the same functionality as 
[transactional callbacks](https://guides.rubyonrails.org/active_record_callbacks.html#transaction-callbacks) of Ruby on 
Rails.

You want to use this if you want to listen on events fired by models within a transaction and you want to be sure the transaction has completed successfully (or is rolled back).


## Installation

You can install the package via composer:

```bash
composer require mvanduijker/laravel-transactional-model-events
```

## Usage

Just add the trait TransactionalAwareEvents to your model or base model.

```php
class MyModel extends Model
{
    use TransactionalAwareEvents;
}
```

The following events will become available:

* `afterCommit.created`
* `afterCommit.saved`
* `afterCommit.updated`
* `afterCommit.deleted`
* `afterCommit.restored`
* `afterCommit.forceDeleted`
* `afterRollback.created`
* `afterRollback.saved`
* `afterRollback.updated`
* `afterRollback.deleted`
* `afterRollback.restored`
* `afterRollback.forceDeleted`

You can add listeners in you EventServiceProvider the same way as normal events

```php
/**
 * The event listener mappings for the application.
 *
 * @var array
 */
protected $listen = [
    'eloquent.afterCommit.created: App\Models\Shipment' => [
        'App\Listeners\SendShipmentNotification',
    ],
];

```

Or you can put them in your model boot method:

```php
class PictureFile extends Model
{
    use TransactionalAwareEvents;
    
    public static function boot()
    {
        parent::boot();
        
        static::registerModelEvent('afterCommit.created', function ($model) {
            if (Storage::exists($model->file)) {
                Storage::delete($model->file);            
            }
        });
    }
}

```

### Testing

``` bash
composer test
```

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.


## Credits

- [Mark van Duijker](https://github.com/mvanduijker)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.