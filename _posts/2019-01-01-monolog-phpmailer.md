---
layout: post
title: "MonologPHPMailer"
date: 2019-01-01 17:58:50 +0100
categories: Projekti
tags: beleženje e-pošta monolog phpmailer
project: https://github.com/filips123/MonologPHPMailer/
technologies: PHP
license: MIT
comments: 1
---

MonologPHPMailer je [PHPMailer][link-phpmailer] odjemalec za [Monolog][link-monolog]. Omogoča pošiljanje dnevniških datotek na e-pošto z PHPMailer.

<!--more-->

## Namestitev

### Zahteve

MonologPHPMailer zahteva vsaj *[PHP][link-php] 5.5.0*, *[Monolog][link-monolog] 1.x ali 2.x* in *[PHPMailer][link-phpmailer] 6.x*.

### S programom Composer

Priporočen način za nameščanje programa je s programom [Composer][link-composer], upravljalcem odvisnosti za PHP.

Dodajte `filips123/monolog-phpmailer` v projektne odvisnosti v `composer.json`. Namestila se bosta tudi Monolog in PHPMailer, vendar je priporočljivo, da ju dodate ročno.

```json
{
    "require": {
        "monolog/monolog": "^1.0",
        "phpmailer/phpmailer": "^6.0",
        "filips123/monolog-phpmailer": "^1.0"
    }
}
```

Ne pozabite zagnati `composer install` in dodati `require 'vendor/autoload.php';` v vašo program.

### Brez programa Composer

Lahko tudi prenesete vse datoteke v mapi [`src`][link-handlers] iz GitHuba in jih nato ročno vključite v svoj program. Prav tako morate ročno namestiti Monolog in PHPMailer.

## Uporaba

V svoj zapisovalec morali dodati odjemalec `MonologPHPMailer\PHPMailerHandler`. Njegov prvi argument mora biti instanca PHPMailer.

## Primer

```php
<?php

use MonologPHPMailer\PHPMailerHandler;

use Monolog\Formatter\HtmlFormatter;
use Monolog\Logger;
use Monolog\Processor\IntrospectionProcessor;
use Monolog\Processor\MemoryUsageProcessor;
use Monolog\Processor\WebProcessor;

use PHPMailer\PHPMailer\PHPMailer;

require __DIR__ . '/vendor/autoload.php';

$mailer = new PHPMailer(true);
$logger = new Logger('logger');

$mailer->isSMTP();
$mailer->Host = 'smtp.example.com';
$mailer->SMTPAuth = true;
$mailer->Username = 'server@example.com';
$mailer->Password = 'password';

$mailer->setFrom('server@example.com', 'Logging Server');
$mailer->addAddress('user@example.com', 'Your Name');

$logger->pushProcessor(new IntrospectionProcessor);
$logger->pushProcessor(new MemoryUsageProcessor);
$logger->pushProcessor(new WebProcessor);

$handler = new PHPMailerHandler($mailer);
$handler->setFormatter(new HtmlFormatter);

$logger->pushHandler($handler);

$logger->error('Error!');
$logger->alert('Something went wrong!');

```

## Različice

Program za različice uporablja [SemVer][link-semver]. Za ogled objavljenih različic obiščite [oznake na skladišču][link-tags].

## Licenca

Program je zaščiten z licenco [MIT][link-license]. Za podrobnosti glejte datoteko [LICENSE][link-license-file].

[link-php]: https://php.net/
[link-monolog]: https://github.com/Seldaek/monolog/
[link-phpmailer]: https://github.com/PHPMailer/PHPMailer/
[link-composer]: https://getcomposer.org/
[link-handlers]: https://github.com/filips123/MonologPHPMailer/tree/master/src
[link-semver]: https://semver.org/
[link-tags]: https://github.com/filips123/MonologPHPMailer/tags/
[link-license]: https://choosealicense.com/licenses/mit/
[link-license-file]: https://github.com/filips123/MonologPHPMailer/blob/master/LICENSE
