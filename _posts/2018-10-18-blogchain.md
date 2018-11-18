---
layout: post
title: "BlogChain"
date: 2018-10-18 15:02:54 +0100
categories: Projekti
tags: decentralizirano blog splet
project: https://github.com/filips123/BlogChain/
technologies: NodeJs Ethereum Web3 IPFS
license: GPL-3.0-or-later
comments: 1
---

![BlogChain Logo](https://vectr.com/filips123/b1Bzz8jXxa.png?width=500&height=100&select=b1Bzz8jXxapage0)

Decentralizirani spletni dnevnik s pomočjo pametnih pogodb Ethereum in Web3.

## Opis

Decentralizirani spletni dnevnik s pomočjo [pametnih pogodb Ethereum](https://www.ethereum.org) in [Web3](https://github.com/ethereum/web3.js). Uporablja [Truffle Framework](http://truffleframework.com) za razvijanje pametnih pogodb in [Bootstrap](https://getbootstrap.com) za spletno stran. Uporablja tudi [IPFS](https://ipfs.io) za spletno gostovanje.

### Značilnosti

- Decentraliziran
- Lahko uporablja katerokoli Ethereum omrežje
- Uporablja IPFS za spletno gostovanje
- Majhna velikost datoteke
- *več značilnosti prihaja ...*

### TODO

- [ ] Brisanje in urejanje prispevkov
- [ ] Brisanje in prenos spletnih dnevnikov
- [ ] Prevodi
- [ ] Boljše testiranje kode
- [ ] Boljša dokumentacija kode
- [ ] JavaScript API

## Kako deluje

TODO

## Uporaba

BlogChain lahko zaženete lokalno, ali pa ga objavite na [IPFS](https://ipfs.io) ali drugo gostovanje.

### Zahteve

You must have [Node.js](https://nodejs.org) and [NPM](https://www.npmjs.com) installed. You also need to install [Truffle Framework](http://truffleframework.com).
You must be connected to the Ethereum blockchain to use the tests. I suggest you use [Ganache](http://truffleframework.com/ganache), which creates a personal Ethereum blockchain.
For web hosting, you can use [IPFS](https://ipfs.io).

### Namestitev

Program lahko namestite iz GitHub skladišča z uporabo `git` ali s prenosom iz [GitHub različic](https://github.com/filips123/BlogChain/releases).
Nato morate prenesti dodatne NPM pakete. BlogChain trenutno uporablja `lite-server` za lokalno spletno gostovanje.

```bash
git clone https://github.com/filips123/BlogChain.git
cd BlogChain
npm install
```

### Poganjanje

Za prevajanje pametnih pogodb zaženite:

```bash
truffle compile
```

Prevedene pogodbe bodo shranjene v mapi `build/contracts`.

Za preizkušanje programa zaženite:

```bash
truffle test
# or
npm test
```

Za to morate biti povezani na Ethereum verigo blokov. Za to priporočam uporabo [Ganache](http://truffleframework.com/ganache).

Za zagon `lite-server` za lokalno spletno gostovanje zaženite:

```bash
npm run dev
```

To bo prevedlo pogodbe in zagnalo strežnik na vratih 3000.

### Objavljanje na IPFS

Spletno stran BlogChain lahko objavite na [IPFS](https://ipfs.io). Najprej ga morate namestiti in nastaviti `path` spremenljivko.

Najprej je potrebno kopirati prevedene pogodbe (`build/contracts/BlogChain.json`) in spletno stran (`src`) v isto mapo.

Nato sledite navodilom v Medium članku [The ultimate end-to-end tutorial to create and deploy a fully decentralized Dapp in ethereum](https://medium.com/@merunasgrincalaitis/the-ultimate-end-to-end-tutorial-to-create-and-deploy-a-fully-descentralized-dapp-in-ethereum-18f0cf6d7e0e#6513) (ne pozabite spremeniti iem mape). Spodaj je njihov povzetek.

Zaženite ukaz:

```bash
ipfs daemon
```

To bo ustvarilo node. V drugi ukazni vrstici ali terminalu zaženite:

```bash
ipfs swarm peers
```

To bo omogočalo deljenje vaše vsebine. Nato zaženite:

```bash
ipfs add -r path/to/website/and/compiled/contract/directory/
```

To bo dodalo vašo mapo v omrežje. Videli boste dolg hash, ki je bil ustvarjen za vas. Zadnji je unikatni identifikator vaše mape:

```
added QmcCZLY7ubZ7pb5hkwSMzazNGkrJpfsHidiEwAi9ep9s7b website/css
added QmPboMFyB7p1rsjcEA8W9TfcQfkUeBhubZQDYPUVtnmXWF website/icons
added QmQGMa9EFZZ29qoL8SnaFcFmY32QKHC7GixxaEyw63aKHv website/js
added Qma1PfCMzemunU9wCTZHCMo6BfgGbMZ1Q3gXpaZTa6uY64 website
```

Kopirajte zadnji hash (primer `Qmc73ZkESUP9sZyU4zGgDMQajfNVLqqKdxPut9GmvStjtJ`) in zaženite:

```bash
ipfs name publish your-last-hash
```

Videli boste nekaj takega:

```
Published to Qmc2LMjSaXPFRvPJCCb4EfctYNLsKE1WTJC7BMxLrN9fmD: /ipfs/Qmc73ZkESUP9sZyU4zGgDMQajfNVLqqKdxPut9GmvStjtJ
```

To pomeni, da bo spletna stran na voljo na URL naslovu od zadnjega hasha (primer `Qmc2LMjSaXPFRvPJCCb4EfctYNLsKE1WTJC7BMxLrN9fmD`. Preverite jo lahko, tako da obiščete `https://gateway.ipfs.io/ipns/<your-hash-here>`.
V mojem primeru je to:

```
https://gateway.ipfs.io/ipns/Qmc2LMjSaXPFRvPJCCb4EfctYNLsKE1WTJC7BMxLrN9fmD
```

Po posodobitvi pogodb ali datotek zaženite:

```bash
ipfs add -r path/to/website/and/compiled/contract/directory/
ipfs name publish your-last-hash
```

Objabljen hash bo vedno enak.

### Nastavitve

Truffle lahko prilagodite v datoteki [truffle-config.js](https://github.com/filips123/BlogChain/blob/master/truffle-config.js). Za več informacij obiščite [Truffle Documentation](http://truffleframework.com/docs/advanced/configuration).

*Več možnosti prihaja ...*

## Uporablja

- [Ethereum](https://www.ethereum.org)
- [Truffle Framework](http://truffleframework.com)
- [Web3](https://github.com/ethereum/web3.js)
- [Bootstrap](https://getbootstrap.com)
- [IPFS](https://ipfs.io)

## Prispevanje

Za prispevanje k projektu si preberite [CONTRIBUTING.md](https://github.com/filips123/BlogChain/blob/master/CONTRIBUTING.md).

## Različice

Program za različice uporablja [SemVer](http://semver.org) SemVer. Za ogled objavljenih različic obiščite [oznake na skladišču](https://github.com/filips123/BlogChain/tags).

## Licenca

Program je zaščiten z licenco [GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.en.html).
