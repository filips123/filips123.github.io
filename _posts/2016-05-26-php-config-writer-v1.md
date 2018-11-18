---
layout: post
title: "PHP Config Writer v1"
date: 2016-05-26 16:29:43 +0200
categories: Projekti
tags: konfiguracija nastavitve
project: https://github.com/filips123/ConfigWriter/
technologies: PHP
license: MIT
comments: 1
---

PHP Config Writer je PHP knjižnjica za enostavno zapisovanje konfiguracijskih datotek v navadni ali razredni obliki.

<!--more-->

**Ta različica je zastarela. Uporabite [novo različico v2](../../../2018/11/17/php-config-writer-v2).**

## Namestitev in uporaba

Vse datoteke, razen `.travis.yml`, `README.md` in `composer.json`, prenesite na strežnik.

### Zapisovanje pdatkov

* Najprej vpišite kodo:

{% highlight php %}
include(''); // Med ' in ' vpišite pot do php-config.php datoteke

$config = new Config;

$config->language(''); // Med ' in '; vpišite jezik (slovenian ali english)
$config->showClass(); // Med ( in ) vpišite ali naj prikaže razred (1 ali 0)
$config->showOther(); // Med ( in ) vpišite ali naj prikaže vrednosti zunaj razreda (1 ali 0)
{% endhighlight %}

* Dodajate lahko tudi komentarje:

{% highlight php %}
$config->comment(''); // Med ' in ' vpišite komentar
{% endhighlight %}

* Vrednosti dodajate s to kodo:

{% highlight php %}
$config->set('', '', ''); // Prvi argument je ime vrednosti, drugi vrednost, tretji pa komentar (po želji)
{% endhighlight %}

* Za zapis v datoteko napišite še:

{% highlight php %}
$data = $config->toString(' ','', ''); // Prvi argument je ime razreda (po želji drugače prazno), drugi je kaj naj bo v razredu (po želji drugače prazno), tretji pa dodatna koda izven razreda (po želji drugače prazno)
$config->toFile('', $data); // Prvi argument je ime datoteke v katero se naj zapiše, drugega pustite privzeto
{% endhighlight %}

### Branje podatkov

* Če ste uporabili razred vpišite:

{% highlight php %}
include('pot_do_datoteke'); // Namesto pot_do_datoteke vpišite pot do datoteke

$razred = new razred; // Namesto razred vpišite ime razreda

echo $razred->$ime_vrednosti; // Namesto razred vpišite ime razreda, namesto ime_vrednosti vpišite ime vrednosti
{% endhighlight %}

* Če niste uporabili razreda vpišite:

{% highlight php %}
include('pot_do_datoteke'); // Namesto pot_do_datoteke vpišite pot do datoteke

echo $ime_vrednosti; // Namesto ime_vrednosti vpišite ime vrednosti
{% endhighlight %}

### Napake

* Če želite pridobiti napako, vpišite:

{% highlight php %}
echo $config->status_message();
{% endhighlight %}

* Če želite pridobiti status, vpišite:

{% highlight php %}
echo $config->status(); // 1 pomeni dokončano, 0 pomeni napaka
{% endhighlight %}
