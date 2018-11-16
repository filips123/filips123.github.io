---
layout: post
title: "Tekmovanje Astro Pi 2017/18 - Ekipa Jakopičevca"
date: 2018-04-01 20:27:23 +0200
categories: Projekti
tags: projekti Python RaspberryPi AstroPi
project: https://github.com/filips123/jakopicevca/
comments: 1
---

Program ekipe Jakopičevca za tekmovanje Astro Pi 2017/18 v misiji Space Lab.

<!--more-->

## Opis

Želela sva raziskati, koliko Slovenije (in drugih držav) je pokrite z gozdovi. Rezultate sva želela primerjati s prejšnjimi slikami pogozdovanja, da bi odkrila krčenje ali celo širjenje gozdov. Prav tako sva želela raziskati svetlobno onesnaženje z nočnimi fotografijami. Za določitev različnih barv na slikah sva uporabila kamero NoIR.

## Kako deluje

Program za določitev lokacije Mednarodne vesoljske postaje (ISS) uporablja modul ephem. Kadar bo ISS leti nad določenimi državami, bo program fotografiral Zemljo na določeno število sekund in fotografije shranil v mapo z imenom lokacije. Ker je možno, da ISS ne bi letel nad določenimi državami, ali pa bi bili lokacijski izračuni napačni, program v vsakem primeru fotografira Zemljo, vendar manj pogosto, in shrani fotografije v mapo `default`. Zaradi analize fotografij program s pomočjo magnetometra shranjuje tudi oddaljenost od severa. Lokacije, podatki s senzorjev in čas se shranjujejo v datoteko CSV.

Lokacije za fotografiranje in druge nastavitve so shranjene v datoteki `cofig.json`. Datoteka vsebuje tudi TLE podatke, zato jih pred zagonom programa posodobite. V razdelku `locations` so shranjene lokacije držav za fotografiranje.  Vrednost `latitude1` je zemljepisna širina najsevernejše točke države, `latitude2` je zemljepisna širina najjužnejše točke države, `longitude1` je zemljepisna širina najzahodnejše točke države, `longitude2` pa je zemljepisna širina najvzhodnejše točke države. Vrednost `delay` je število sekund med posameznimi fotografijami. V razdelku `default` so shranjene informacije o fotografiranju, kadar ISS ne leti nad nobeno državo. Vrednost `delay` je število sekund med posameznimi fotografijami, `fallbackDelay` pa je število sekund med posameznimi fotografijami, kadar pride do napake pri pridobivanju lokacije ISS.

## Uporaba

Program mora biti zagnan na Raspberry Pi. Program je namenjen uporabi na ISS, vendar je lahko z nekaterimi prilagoditvami primeren tudi za druga okolja.

### Zahteve

Program uporablja Python 3 in ni bil preizkušen na Python 2. Uporablja naslednje Python module:

* sense-hat
* picamera
* ephem

### Namestitev

Program je priporočljivo namestiti v Python VENV, ki mora biti ustvarjen z argumentom `-sistem-site-packages, vendar so tukaj splošna navodila za namestitev.

Namestitev iz PyPI:

{% highlight shell %}
sudo pip3 install jakopicevca
{% endhighlight %}

Namestitev iz GitHub skladišča:

{% highlight shell %}
git clone https://github.com/filips123/jakopicevca/
cd jakopicevca
sudo python3 setup.py install
{% endhighlight %}

### Zagon

Ustvarite datoteko `config.json` z naslednjo vsebino (dopolnite manjkajoče informacije):

{% highlight json %}
{
  "TLE": [
    "ISS (ZARYA)",
    "### Pridobite ISS TLE podatke iz ###",
    "### https://www.celestrak.com/NORAD/elements/stations.txt ###"
  ],

  "locations": {
      "### Ime lokacije ###": {
      "latitude1": najsevernejsa-tocka,
      "latitude2": najjuznejsa-tocka,
      "longitude1": najzahodnejsa-tocka,
      "longitude2": najvzhodnejsa-tocka,
      "delay": premor-med-fotografijami
      }
  },

  "default": {
    "delay": privzeti-premor-med-fotografijami,
    "fallbackDelay": nadomestni-premor-med-potografijami
  }
}
{% endhighlight %}

Shranite to datoteko in zaženite program z:

{% highlight shell %}
python3 -m jakopicevca pot/do/config.json pot/do/datoteke.csv pod/do/mape/s/fotografijami pot/do/datoteke.log
{% endhighlight %}

Datoteki CSV in log, in mapa s fotografijami bodo ustvarjeni samodejno.

## Licenca

Program je zaščiten z licenco [GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.en.html).
