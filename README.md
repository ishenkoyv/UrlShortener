URL shortener library
=====================

This library allows you to shorten a URL, reverse is also possible.

[![Build Status](https://api.travis-ci.org/mremi/UrlShortener.png?branch=master)](https://travis-ci.org/mremi/UrlShortener)
[![Total Downloads](https://poser.pugx.org/mremi/url-shortener/downloads.png)](https://packagist.org/packages/mremi/url-shortener)
[![Latest Stable Version](https://poser.pugx.org/mremi/url-shortener/v/stable.png)](https://packagist.org/packages/mremi/url-shortener)

**Basic Docs**

* [Installation](#installation)
* [Bit.ly API](#bitly-api)
* [Chain providers](#chain-providers)

<a name="installation"></a>

## Installation

Only 1 step:

### Download UrlShortener using composer

Add UrlShortener in your composer.json:

```js
{
    "require": {
        "mremi/url-shortener": "dev-master"
    }
}
```

Now tell composer to download the library by running the command:

``` bash
$ php composer.phar update mremi/url-shortener
```

Composer will install the library to your project's `vendor/mremi` directory.

<a name="bitly-api"></a>

## Bit.ly API

```php
<?php

use Mremi\UrlShortener\Http\ClientFactory;
use Mremi\UrlShortener\Provider\Bitly\BitlyProvider;
use Mremi\UrlShortener\Provider\Bitly\OAuthClient;

$bitlyProvider = new BitlyProvider(new ClientFactory, new OAuthClient(new ClientFactory, 'username', 'password'));

$shortened = $bitlyProvider->shorten('http://www.google.com');

$expanded  = $bitlyProvider->expand('http://bit.ly/ze6poY');
```

<a name="chain-providers"></a>

## Chain providers

```php
<?php

use Mremi\UrlShortener\Http\ClientFactory;
use Mremi\UrlShortener\Provider\Bitly\BitlyProvider;
use Mremi\UrlShortener\Provider\Bitly\OAuthClient;
use Mremi\UrlShortener\Provider\ChainProvider;

$chainProvider = new ChainProvider;

$bitlyProvider = new BitlyProvider(new ClientFactory, new OAuthClient(new ClientFactory, 'username', 'password'));

$chainProvider->addProvider($bitlyProvider);

$shortened = $chainProvider->getProvider('bitly')->shorten('http://www.google.com');

$expanded  = $chainProvider->getProvider('bitly')->expand('http://bit.ly/ze6poY');
```
