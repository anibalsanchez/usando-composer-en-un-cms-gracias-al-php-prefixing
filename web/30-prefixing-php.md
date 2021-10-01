# Prefixing PHP <!-- .slide: class="p-small" -->

Case 1: Sample snippet of code from `nesbot/carbon`, a simple PHP API extension for DateTime.

```php
namespace Carbon;

use Carbon\Exceptions\InvalidDateException;
use DateInterval;
use Symfony\Component\Translation;

class Carbon extends DateTime
{
    const NO_ZERO_DIFF = 01;
```


## Prefixing PHP Namespaces<!-- .slide: class="p-small" -->

Case 1: Prefixed snippet of code from `nesbot/carbon`, with `Extly` prefix.

```php
namespace Extly\Carbon;

use Extly\Carbon\Exceptions\InvalidDateException;
use DateInterval;
use Extly\Symfony\Component\Translation;

class Carbon extends DateTime
{
    const NO_ZERO_DIFF = 01;
```


## Prefixing PHP - Case 2<!-- .slide: class="p-small" data-visibility="hidden" -->

Case 2: Sample snippet of code from Laravel's `illuminate/support` library.

```php
use Illuminate\Container\Container;

if (! function_exists('abort')) {
    function abort($code, $message = '')
    {
        return app()->abort($code, $message, $headers);
...

if (! function_exists('app')) {
    function app($make = null)
```


## Prefixing PHP <!-- .slide: class="p-small" data-visibility="hidden" -->

Case 2: Prefixed snippet of code from Laravel's `illuminate/support` library, with `XT_` prefix.

```php
use Extly\Illuminate\Container\Container;

if (! function_exists('XT_abort')) {
    function XT_abort($code, $message = '')
    {
        return XT_app()->abort($code, $message, $headers);
...

if (! function_exists('XT_app')) {
    function XT_app($make = null)
```


## The first Real-world Case <!-- .slide: class="p-small" -->

Pimple `pimple/pimple`, a simple Dependency Injection Container, used in Akeeba's FOF.

```php [9]
<?php
/*
 * This file is part of Pimple.
 *
 * Copyright (c) 2009 Fabien Potencier
...
 */

namespace FOF30\Pimple;

defined('_JEXEC') || die;

use ArrayAccess;
use InvalidArgumentException;
use RuntimeException;
use SplObjectStorage;

/**
 * Container main class.
 *
 * @author  Fabien Potencier
 */
class Container implements ArrayAccess
{
...
```


## Can we prefix entire projects? <!-- .slide: class="list-small" -->

We need to prefix automatically:

- Full libraries
- Namespaces and objects in the global scope
- Automated tests
- Different libraries versions
- Code for different PHP versions


## Introducing PHP Prefixer <!-- .slide: class="p-small" -->

![Introducing PHP Prefixer](images/30-prefixing-php/php-prefixer.png)<!-- .element: class="w-80" style="border-radius: .25rem; border-width: 1px; border-color: #aaa; border-style: solid;" -->

https://php-prefixer.com/ - Launched on Nov 2020


## Let's prefix an extension <!-- .slide: data-background-repeat="no-repeat" data-background-image="images/10-what-is-composer/logomark.min.svg" data-background-size="8% auto" data-background-position="90% 10%" class="list-small" -->

[anibalsanchez/xt-laravel-starter-for-joomla](https://github.com/anibalsanchez/xt-laravel-starter-for-joomla)

XT Laravel Starter for Joomla<!-- .element: class="small" -->


## Let's prefix an extension <!-- .slide: data-background-repeat="no-repeat" data-background-image="images/10-what-is-composer/logomark.min.svg" data-background-size="8% auto" data-background-position="90% 10%" class="list-small" -->

The `composer.json` with the prefix definitions:

```json
...
    "extra": {
        "php-prefixer": {
            "project-name": "XT Laravel Starter for Joomla",
            "prefix-for-namespaces": "Extly",
            "prefix-for-global-objects": "XT_"
        }
    },
    "autoload": {
        "psr-4": {
            "App\\": "app/",
...
```


## Prefixing PHP - Create

![Let's build an extension - Demo](images/30-prefixing-php/php-prefixer.com_service_resources_projects-01.png)<!-- .element: style="heigth: 80%" -->


## Prefixing PHP - Upload <!-- .slide: data-visibility="hidden" -->

![Let's build an extension - Demo](images/30-prefixing-php/php-prefixer.com_service_resources_projects-02.png)<!-- .element: style="heigth: 80%" -->


## Prefixing PHP - Validate <!-- .slide: data-visibility="hidden" -->

![Let's build an extension - Demo](images/30-prefixing-php/php-prefixer.com_service_resources_projects-03.png)<!-- .element: style="heigth: 80%" -->


## Prefixing PHP - Process <!-- .slide: data-visibility="hidden" -->

![Let's build an extension - Demo](images/30-prefixing-php/php-prefixer.com_service_resources_projects-04.png)<!-- .element: style="heigth: 80%" -->


## Prefixing PHP - Download

![Let's build an extension - Demo](images/30-prefixing-php/php-prefixer.com_service_resources_projects-05.png)<!-- .element: style="heigth: 80%" -->


## Prefixing PHP - Testing

```php
~/vendor_prefixed/monolog/monolog$ phpunit
PHPUnit 5.7.27 by Sebastian Bergmann and contributors.

................................................................. 65 / 97 ( 67%)
................................                                  97 / 97 (100%)

Time: 116 ms, Memory: 6.00MB
```


## Prefixing PHP - Results

```php [11-13]
<?php
/* This file has been prefixed by <PHP-Prefixer> for "XT Laravel Starter for Joomla" */

/**
 * This file is part of the Carbon package.
 *
 * (c) Brian Nesbitt <brian@nesbot.com>
 *
...
 */
namespace Extly\Carbon;

use Extly\Carbon\Traits\Date;
use DateTime;
use DateTimeInterface;
use DateTimeZone;

/**
 * A simple API extension for DateTime.
 *
...
 */
class Carbon extends DateTime implements CarbonInterface
{
    use Date;

    /**
     * Returns true if the current class/instance is mutable.
     *
     * @return bool
     */
    public static function isMutable()
    {
        return true;
    }
}
```

[xt-laravel-starter-for-joomla-library/blob/prefixed/vendor_prefixed/nesbot/carbon/src/Carbon/Carbon.php](https://github.com/anibalsanchez/xt-laravel-starter-for-joomla-library/blob/prefixed/vendor_prefixed/nesbot/carbon/src/Carbon/Carbon.php)<!-- .element: class="small" -->