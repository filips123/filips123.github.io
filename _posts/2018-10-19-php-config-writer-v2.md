---
layout: post
title: "PHP Config Writer v2"
date: 2018-11-19 20:16:32 +0200
categories: Projekti
tags: konfiguracija nastavitve
project: https://github.com/filips123/ConfigWriter/
technologies: PHP
license: MIT
comments: 1
redirect_from:
  - /2016/05/26/php-config
  - /2016/05/26/php-config-writer
---

PHP Config Writer je PHP knjižnjica za enostavno zapisovanje konfiguracijskih datotek.

<!--more-->

## Namestitev

### Zahteve

PHP Config Writer potrebuje  vsaj *[PHP][link-php] 5.5.9*.
Za shranjevanje konfiguracijske datoteke mora imeti spletni strežnik zapisovalni dostop do mape s konfiguracijsko datoteko.

### S programom Composer

Priporočen način za nameščanje programa je s programom [Composer][link-composer], upravljalcem odvisnosti za PHP.

V projekt je potrebno dodati `filips123/config-writer`.

```bash
composer require filips123/config-writer:^2.0
```

Nato boste v vaš program morali samo vključiti autoloader in namepace.

```php
<?php

use ConfigWriter\Config;

require 'vendor/autoload.php';

$config = new Config;
```

## Brez programa Composer

Lahko tudi prenesete datoteke iz GitHuba in jih ročno vključite v vaše datoteke.

Nato boste v vaš program morali vključiti vse datoteke in namepace.

```php
<?php

use ConfigWriter\Config;

require 'src/Exceptions/UnsupportedFormatException.php';
require 'src/Exceptions/WriteException.php';
require 'src/ConfigInterface.php';
require 'src/AbstractConfig.php';
require 'src/Config.php';
require 'src/Record.php';
require 'src/Writers/WriterInterface.php';
require 'src/Writers/PhpWriter.php';

$config = new Config;
```

## Uporaba

### Ustvarjanje konfiguracije

Ustvarjanje konfiguracije je možno z razredom `ConfigWriter\Config`.

```php
$config = new Config;
```

Konstruktor sprejme dva parametra, podatke in komentar, ki pa nista zahtevana.
Parameter s podatki lahko vsebuje prenastavljene podatke za konfiguracijo, komenrar pa dodatni komentar (ali kodo), ki bo vključen na vrh generiranje datoteke.

```php
$config = new Config(
    [
        'username' => 'user',
        'password' => 'pass',
    ],
    <<<EOD
/**
 * The configuration file.
 *
 * It contains configuration data.
 */
EOD;
);
```

### Dodajanje zapisov

Dodajanje zapisov je možno z metodo `ConfigWriter\Config::addRecord()`.

```php
$config->addRecord('application', 'ConfigWriter');
```

Zapisi lahko vsebujejo tudi komentar, ki bo vključen v konfiguracijo.

```php
$config->addRecord('application', 'ConfigWriter', 'Application name');
```

### Dodajanje odsekov

Odseki vizualno in funkcionalno delijo zapise ali skupine zapisov. Dodani so lahko z metodo `ConfigWriter\Config::addSection()`.

```php
$database = $config->addSection('database', [], 'Database settings');

$database->addRecord('host', 'localhost', 'Database host');
$database->addRecord('port', '3306', 'Database port');
```

Tudi odseki lahko vsebujejo predefiniranje podatke in komentar.

```php
$config->addSection(
    'database',
    [
        'host' => 'localhost',
        'port' => '3306',
    ],
    'Database settings');
```


### Shranjevanje konfiguracije

Konfiguracijo lahko shranite z metodama `ConfigWriter\Config::toString()` in `ConfigWriter\Config::toFile()`.

Pri shranjevanju v niz je zapisovalec zahtevan, pri shranjevanju v datoteko pa bo samodejno določen.

```php
$config->toString(new ConfigWriter\Writers\PhpWriter);
$config->toFile('config.php');
```

Zapisovalci lahko omogočajo tudi dodatne zapisovalne možnosti. Njihovo spreminjanje lahko trenutno povzroči nestabilno delovanje programa.

```php
$config->toFile('config.php', new ConfigWriter\Writers\PhpWriter, ['indentation' => '	']);
```

Trenutno edini podprt zapisovalec je za PHP array, vendar bo več zapisovalcev dodanih kasneje.

## Različice

Program za različice uporablja [SemVer][link-semver]. Za ogled objavljenih različic obiščite [oznake na skladišču][link-tags].

## Licenca

Program je zaščiten z licenco [MIT][link-license].

[link-license]: https://choosealicense.com/licenses/mit/
[link-php]: https://php.net/
[link-composer]: https://getcomposer.org/
[link-semver]: https://semver.org/
[link-tags]: https://github.com/filips123/ConfigWriter/tags/
