---
layout: post
title:  "PHP config"
date:   2015-05-26 16:29:43 +0200
categories: Projekti
tags: projekti PHP konfiguracija
comments: 1
---
PHP config je PHP paket za enostavno zapisovanje konfiguracijskih datotek v navadni ali razredni obliki. Na voljo je na spletni strani [https://github.com/filips123/php-config/](https://github.com/filips123/php-config/).

<!--more-->

## Namestitev
Vse datoteke razen README.md prenesite na strežnik.

## Uporaba
### Zapisovanje pdatkov
* Najprej vpišite kodo:
{% highlight php %}
<?php
include(''); //Med ' in ' vpišite pot do php-config.php datoteke.
$config = new Config;
$config->language(''); //Med ' in '; vpišite jezik (slovenian ali english)
$config->showClass(); //Med ( in ) vpišite ali naj prikaže razred (1 ali 0).
$config->showOther(); //Med ( in ) vpišite ali naj prikaže vrednosti zunaj razreda (1 ali 0).
{% endhighlight %}
  
* Dodajate lahko tudi komentarje:
{% highlight php %}
$config->comment(''); //Med ' in ' vpišite komentar.
{% endhighlight %}
  
* Vrednosti dodajate s to kodo:
{% highlight php %}
$config->set('','','')//Prvi argument je ime vrednosti, drugi vrednost, tretji pa komentar (po želji).
{% endhighlight %}
  
* Za zapis v datoteko napišite še:
{% highlight php %}
$data = $config->toString('','',''); //Prvi argument je ime razreda (po želji drugače prazno), drugi je kaj naj bo v razredu (po želji drugače prazno), tretji pa dodatna koda izven razreda (po želji drugače prazno).
$config->toFile('',$data); //Prvi argument je ime datoteke v katero se naj zapiše, drugega pustite privzeto.
?>
{% endhighlight %}

### Branje podatkov
* Če ste uporabili razred vpišite:
{% highlight php %}
<?php
include('pot_do_datoteke'); //Namesto pot_do_datoteke vpišite pot do datoteke.
$razred = new razred; //Naesto razred vpišite ime razreda.
$razred->$ime_vrednosti; //Namesto razred vpišite ime razreda, namesto ime_vrednosti vpišite ime vrednosti. Ta koda ne vrača vrednosti.Za izpis uporabite echo ali print.
?>
{% endhighlight %}
  
* Če niste uporabili razreda vpišite:
{% highlight php %}
<?php
include('pot_do_datoteke'); //Namesto pot_do_datoteke vpišite pot do datoteke.
$ime_vrednosti; //Namesto ime_vrednosti vpišite ime vrednosti. Ta koda ne vrača vrednosti.Za izpis uporabite echo ali print.
?>
{% endhighlight %}

### Napake
* Če želite pridobiti napako, vpišite:
{% highlight php %}
<?php
echo $config->status_message();
?>
{% endhighlight %}

* Če želite pridobiti status, vpišite:
{% highlight php %}
<?php
echo $config->status(); //1 pomeni dokončano, 0 pomeni napaka.
?>
{% endhighlight %}