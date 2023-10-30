---
layout: post
categories: ["Domotique"]
date: 2023-10-29 22:34:00
title: "Home Assistant - Installation et configuration"
---

Je mets ici mes différentes notes pour l’installation et la configuration de mon home assistant. Mon thermostat centralisé CPL commençant à faire n’importe quoi j’ai dû trouver une solution de remplacement. J’ai décidé d’utiliser [Home Assistant](https://www.home-assistant.io/) sur un Raspberry Pi. Ce billet sera modifié au fur et à mesure de mes modifications, mon but est plus d’avoir un accès pratique à mes notes, pas vraiment de vous faire un tuto pour vous mais plus de faire un tuto pour moi-même. Mais bon, si ça vous est utile, tant mieux.

![RPI](/assets/images/domotique/haos.webp){: width="200" style="display: block; margin: 0 auto"}

<!--more-->

<!--
██████╗  █████╗ ███████╗██████╗ ██████╗ ███████╗██████╗ ██████╗ ██╗   ██╗    ██████╗ ██╗
██╔══██╗██╔══██╗██╔════╝██╔══██╗██╔══██╗██╔════╝██╔══██╗██╔══██╗╚██╗ ██╔╝    ██╔══██╗██║
██████╔╝███████║███████╗██████╔╝██████╔╝█████╗  ██████╔╝██████╔╝ ╚████╔╝     ██████╔╝██║
██╔══██╗██╔══██║╚════██║██╔═══╝ ██╔══██╗██╔══╝  ██╔══██╗██╔══██╗  ╚██╔╝      ██╔═══╝ ██║
██║  ██║██║  ██║███████║██║     ██████╔╝███████╗██║  ██║██║  ██║   ██║       ██║     ██║
╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚═╝     ╚═════╝ ╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝       ╚═╝     ╚═╝
-->

# Raspberry Pi

![RPI](/assets/images/domotique/rpi.svg){: width="200" style="display: block; margin: 0 auto"}

## Achat

Au moment de l’achat le RPi était à un prix effroyable, j’ai voulu me rabattre sur un autre PC fanless. Mais tout ceux que je trouvais avait un ventilateur (fanless ???) ou un prix aussi élevé que le RPi… J’ai donc choisi d’acheter un RPi 4 8Go de Ram, une carte μsd de 128Go et un ZkeeShop Boitier en Aluminium. L’ensemeble me coûte 299,94€ (total provisoire : 325,20€). Je passe commande le 25 janvier vers 1h du matin, je le reçois le 26 janvier !

## Installation HAOS

J’ai téléchargé HAOS pour Rpi via [la  la page dédiée](https://www.home-assistant.io/installation/raspberrypi/).

```sh
unxz --keep /tmp/haos_rpi4-64-9.4.img.xz 	# décompression
ls -l /dev/disk/by-id			# identification de la carte μsd (ici sdc)
sudo dd if='/tmp/haos_rpi4-64-9.4.img' of=/dev/sdc bs=256M status=progress && sync

```

Je mets la carte μsd dans le Rpi, je le branche en ethernet et je l’alimente. Je trouve l’IP via freebox-os et depuis mon PC, dans mon navigateur web : http://192.168.0.41:8123 (les adresse homeassistant.local:8123 et homeassistant:8123 ne fonctionne pas, mon réseau est configuré de façon trop strict ?)

## Configuration (onboarding)

* Nom, mot de passe,…
* Pays : **FR**
* Langue : **fr**
* Fuseau horaire : **Europe/Paris**
* Élévation : **0**
* Système unitaire : **Métrique, Celsius, kilogrammes**
* Devise : **EUR**
* Share anonymized : **Tout off**

Ajout des différents appareils détectés

## Paramètres

Création d’un compte pour chaque membre de la famille

## Téléphone

J’ajoute sur mon téléphone, l’application [Home Assistant via F-droid](https://f-droid.org/fr/packages/io.homeassistant.companion.android.minimal/)

## Freebox

Je défini une ip fixe pour le Rpi dans le [gestionnaire de ma freebox](http://mafreebox.freebox.fr/)

Ici ce termine la première étape de configuration du Rpi


<!--
████████╗██╗  ██╗███████╗██████╗ ███╗   ███╗ ██████╗ ███╗   ███╗███████╗████████╗██████╗ ███████╗███████╗
╚══██╔══╝██║  ██║██╔════╝██╔══██╗████╗ ████║██╔═══██╗████╗ ████║██╔════╝╚══██╔══╝██╔══██╗██╔════╝██╔════╝
   ██║   ███████║█████╗  ██████╔╝██╔████╔██║██║   ██║██╔████╔██║█████╗     ██║   ██████╔╝█████╗  ███████╗
   ██║   ██╔══██║██╔══╝  ██╔══██╗██║╚██╔╝██║██║   ██║██║╚██╔╝██║██╔══╝     ██║   ██╔══██╗██╔══╝  ╚════██║
   ██║   ██║  ██║███████╗██║  ██║██║ ╚═╝ ██║╚██████╔╝██║ ╚═╝ ██║███████╗   ██║   ██║  ██║███████╗███████║
   ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝╚═╝     ╚═╝ ╚═════╝ ╚═╝     ╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚══════╝╚══════╝
-->

# Thermomètres/Hydromètres

![LYWSD03MMC](/assets/images/domotique/LYWSD03MMC.webp){: width="300" style="display: block; margin: 0 auto"}

20 janvier 2023, achat de 5 thermomètres/hydromètres bluetooth Xiaomi (LYWSD03MMC) 25,26€ (frais de port inclus). Je n’ai pas trouvé de thermomètre/Hydromètre connecté moins cher. Je souhaite les hacker en suivant les indications de [hackaday](https://hackaday.com/2020/11/17/custom-firmware-for-cheap-bluetooth-thermometers/). Il est même possible de directement passer par [une page web pour le hack](https://atc1441.github.io/TelinkFlasher.html) ! Ceci permet d’utiliser ces thermomètres/hydromètres très bon marché sans passer par l’application propriétaire (ce qui me semble important), directement dans home assistant. Par défaut le flux est chiffré. Cette technique m’évite la fabrication de capteur BLE utilisant ESP32/DHT11…

Le 6 février 2023, je reçois les 5 thermomètres.

J’allume le premier et suis [les instructions](https://www.youtube.com/watch?v=NXKzFG61lNs) :
1. Depuis mon téléphone, via chrome (qui a les autorisations de recherche d’appareils contrairement à mon habituel Firefox), je vais sur la page [TelinkFlasher](https://atc1441.github.io/TelinkFlasher.html)
2. Téléchargement du firmware.bin (dans mon cas Release 78)
3. Clic sur Connect
4. Sélection de LYWSD03MMC, Associer
5. Attente que la connection est ok (en bas de la page)
6. « Do activation » Récupération des informations
7. Pour **1** (chambre parents) :
	Mi token : 619b56772b******cc23b76
	Mi Bind Key : 9a0afe132c692f86eb******06429
	Après flash, devient : ATC_6C9727
	Mac : AA:BB:CC:DD:EE:FF
	Après flash, je reconnecte le thermomètre pour mettre "Advertising interval" à 10 minutes pour économiser la batterie
8. Start flashing (après avoir sélectionné le fichier bin)
9. Il est directement trouvé par Home assistant. Je procède de la même façon pour les autres détecteurs. Le firmware indique de temps en temps, le niveau de batterie, ce qui est une information sympatique… Je les nomme sans les désignations originales (LYWSD03MMC) et préfère « Temp/Humidity [1] 6C9727 », etc

<!-- 7 février, bon, ils sont directement vu par home assistant mais il ne sont pas reconnus comme des détecteurs directement utilisables. Certains sites ([1](https://www.youtube.com/watch?v=l5ea7lQWpMk) ou [2](https://www.youtube.com/watch?v=CWPlFVxNZmc)) indiquent des solutions avec ESPHome (que j’installe ce jour dans mon home assistant), [un autre](https://community.home-assistant.io/t/xiaomi-mi-ble-temp-sensor-not-registering-on-ha/427252) indique [BLE Monitor](https://github.com/custom-components/ble_monitor) ou [Theengs Gateway](https://gateway.theengs.io/).

J’essaye ce dernier. Pour cela, j’ajoute son dépot **https://github.com/mihsu81/addon-theengsgw** dans modules complémentaires (☰ → Dépots), il n’apparait qu’après redémarrage de HAOS.
Clic sur Installer. TheengsGateway apparait ensuite dans "Appareils et services", onglet Appareils. Dans configuration de TheegsGateway, il va falloir trouver les bons paramètres et j’ai bien l’impression que l’extension n’est utilisable que si Mosquitto broker add-on est installé et configuré. Même après avoir installé Mosquitto, je continue à penser que je vais galérer…

-->

8 février, je vais faire une tentative via BLE en suivant la vidéo [Home Assistant Xiaomi Temperature & Humidity Sensor integration (HOW-TO)](https://www.youtube.com/watch?v=y2yW2czWJcc) ([article correspondant](https://peyanski.com/home-assistant-xiaomi-temperature-humidity-sensor/)).

Première étape simplifiant l’installation, passer par HACS…

## Installation de HACS

Je suis [How to install & use Home Assistant Community Store (HACS) | TUTORIAL](https://peyanski.com/how-to-install-home-assistant-community-store-hacs/) et sa [version vidéo youtube](https://youtu.be/QPXxMSV3BUY)
1. Installer le module « Terminal & SSH » (de toute façon, c’est un module qui me semble intéressant, mais quand même… ça me rappelle de plus en plus l’[intro de l’épisode « Sueurs froides » de Malcolm](https://youtu.be/-kDtVGdkyfY)…
2. Dans l’invite ssh : $ wget -q -O - https://install.hacs.xyz | bash -
3. Redémarrage de HAOS
4. c > Intégrations, « Ajouter une intégration », chercher « hacs »
5. Configurer HACS et activer AppDeamon et NetDeamon

## Passive BLE Monitor custom component

1. HACS → Intégrations → Explorer et Télecharger des dépôts → Rechercher « Passive BLE monitor integration »
2. Cliquer sur « Télécharger »
3. Redémarrer HAOS
4. Paramètres → Appareils et Services → Intégrations → + Ajouter une intégration → BLE
5. Je coche « Restaurer l'état après un redémarrage » et entre dans le menu « - Devices - » → « Add device… »

(Inutile de saisir, HAOS a déjà renseigné mes thermomètres, j’en profite pour noter les adresses mac complètes des entrées. Au pire, j’aurais pu me connecter dans l’interface ssh, pour lancer :
```sh
$ bluetoothctl
[bluetooth]# scan on
info <mac_adress>
```
)

Les thermomètres peuvent être configurés dans HAOS, pour l’instant je me contente d’ajouter les températures sur ma page d’accueil. Je pourrais également mettre la batterie et/ou l’humidité. Pour l’instant, ces informations ne me semblent pas très importantes. Je m’adapterais en fonction de ce que le module thermostat affiche et n’affiche pas.
