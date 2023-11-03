---
layout: post
categories: ["Domotique"]
date: 2023-10-29 22:34:00
title: "Home Assistant - Installation et configuration"
---

Je mets ici mes différentes notes pour l’installation et la configuration de mon Home Assistant. Mon thermostat centralisé CPL commençant à faire n’importe quoi j’ai dû trouver une solution de remplacement. J’ai décidé d’utiliser [Home Assistant](https://www.home-assistant.io/) sur un Raspberry Pi. Ce billet sera modifié au fur et à mesure de mes modifications, mon but est plus d’avoir un accès pratique à mes notes, pas vraiment de vous faire un tuto pour vous mais plus de faire un tuto pour moi-même. Mais bon, si ça vous est utile, tant mieux.

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

Au moment de l’achat le RPi était à un prix effroyable, j’ai voulu me rabattre sur un autre PC fanless. Mais tout ceux que je trouvais avait un ventilateur (fanless ???) ou un prix aussi élevé que le RPi… J’ai donc choisi d’acheter un RPi 4 8Go de Ram, une carte μsd de 128Go et un ZkeeShop Boitier en Aluminium. L’ensemeble me coûte 299,94€ (total provisoire : 325,20€). Je passe commande le 25 janvier vers 1h du matin, je le reçois le 26 janvier ! Si j’avais pu attendre la sortie du Raspberry Pi 5, ça m’aurait coûté bien moins pour de meilleurs performances…

## Installation HAOS

J’ai téléchargé HAOS pour Rpi via [la  la page dédiée](https://www.home-assistant.io/installation/raspberrypi/).

```sh
unxz --keep /tmp/haos_rpi4-64-9.4.img.xz 	# décompression
ls -l /dev/disk/by-id			# identification de la carte μsd (ici sdc)
sudo dd if='/tmp/haos_rpi4-64-9.4.img' of=/dev/sdc bs=256M status=progress && sync
```

Je mets la carte μsd dans le Rpi, je le branche en ethernet et je l’alimente. Je trouve l’IP via [freebox-os](http://mafreebox.freebox.fr).

Depuis le navigateur web de mon PC j’accède à HAOS via [http://192.168.0.41:8123](http://192.168.0.41:8123)

Les adresses [homeassistant.local:8123](homeassistant.local:8123) et [homeassistant:8123](homeassistant:8123) ne fonctionnent pas. C’est dommage car ce sont des adresses faciles à retenir, mon réseau est peut-être mal configuré, il faudra que j’investigue.

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

## Portée du bluetooth

Si j’avais choisi des thermomètres zigbee, chacun de ceux-ci amélioreraient la couverture réseau de la maison. Comme j’ai choisi des thermomètres bluetooth, je dois placer le Raspberry Pi le plus au centre possible de la maison afin d’atteindre la chambre du plus jeune.

## Wifi

Par défaut, j’avais configuré la connexion réseau du Raspberry Pi en éthernet. Pour passer en wifi :

* Paramètres → Système → Réseau → WLAN0
* IPv4 DCHP

Une fois la config faite, ne pas oublier que l’adresse IP définie jusqu’alors dans la freebox l’était pour l’adresse mac de la carte ethernet !

## Paramètres

Création d’un compte pour chaque membre de la famille

## Téléphone

J’ajoute sur mon téléphone, l’application [Home Assistant via F-droid](https://f-droid.org/fr/packages/io.homeassistant.companion.android.minimal/)

## Freebox

Je défini une ip fixe pour le Rpi dans le [gestionnaire de ma freebox](http://mafreebox.freebox.fr/). Ici ce termine la première étape de configuration du Rpi


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

20 janvier 2023, achat de 5 thermomètres/hydromètres bluetooth Xiaomi (LYWSD03MMC) 25,26€ (frais de port inclus). Je n’ai pas trouvé de thermomètre/Hydromètre connecté moins cher. Je souhaite les "hacker" en suivant les indications de [hackaday](https://hackaday.com/2020/11/17/custom-firmware-for-cheap-bluetooth-thermometers/). Il est même possible de directement passer par [une page web pour le hack](https://atc1441.github.io/TelinkFlasher.html) ! Ceci permet d’utiliser ces thermomètres/hydromètres très bon marché sans passer par l’application propriétaire (ce qui me semble important), directement dans Home Assistant. Par défaut le flux est chiffré. Cette technique m’évite la fabrication de capteur BLE utilisant ESP32/DHT11…

6 février 2023, j’ai reçu les 5 thermomètres.

## Flash du firmware

J’allume le premier et suis [les instructions](https://www.youtube.com/watch?v=NXKzFG61lNs) :
1. Depuis mon téléphone, via chrome (qui a les autorisations de recherche d’appareils contrairement à mon habituel Firefox), je vais sur la page [TelinkFlasher](https://atc1441.github.io/TelinkFlasher.html)
2. Téléchargement du firmware.bin (dans mon cas Release 78)
3. Clic sur Connect
4. Sélection de LYWSD03MMC, Associer
5. Attente que la connection est ok (en bas de la page)
6. « Do activation » Récupération des informations
7. Pour 1️⃣ (chambre parents) :
	* Mi token : 619b56772b******cc23b76
	* Mi Bind Key : 9a0afe132c692f86eb******06429
	* Après flash, devient : ATC_6C9727
	* Mac : AA:BB:CC:DD:EE:FF
	* Après flash, je reconnecte le thermomètre pour mettre "Advertising interval" à 10 minutes pour économiser la batterie
8. Start flashing (après avoir sélectionné le fichier bin)
9. Il est directement trouvé par Home Assistant. Je procède de la même façon pour les autres détecteurs. Le firmware indique de temps en temps, le niveau de batterie, ce qui est une information sympatique… Je les nomme sans les désignations originales (LYWSD03MMC) et préfère « Temp/Humidity [1] 6C9727 », etc

Je fais ensuite de même pour 2️⃣,3️⃣,4️⃣ et 5️⃣.

7 février, ils sont directement vu par Home Assistant mais il ne sont pas reconnus comme des détecteurs directement utilisables.

8 février, [Passive BLE Monitor integration](https://github.com/custom-components/ble_monitor) semble la meilleure solution. Je vais suivre la vidéo [Home Assistant Xiaomi Temperature & Humidity Sensor integration (HOW-TO)](https://www.youtube.com/watch?v=y2yW2czWJcc) ([article correspondant](https://peyanski.com/home-assistant-xiaomi-temperature-humidity-sensor/)). Pour installer ce composant, le plus simple est de passer par HACS. Pour installer HACS, il faut passer par Terminal & SSH, qu’il faut que j’installe… 

<iframe width="560" height="315" style="display: block; margin: 20px auto" src="https://www.youtube.com/embed/-kDtVGdkyfY?si=zuWPwPYCcfGVkivp" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Installation de HACS

Je suis [How to install & use Home Assistant Community Store (HACS) | TUTORIAL](https://peyanski.com/how-to-install-home-assistant-community-store-hacs/) et sa [version vidéo youtube](https://youtu.be/QPXxMSV3BUY)
1. Installer le module « Terminal & SSH » (de toute façon, c’est un module qui me semble intéressant, mais quand même… ça me rappelle de plus en plus l’[intro de l’épisode « Sueurs froides » de Malcolm](https://youtu.be/-kDtVGdkyfY)…
2. Dans l’invite ssh :
```sh
$ wget -q -O - https://install.hacs.xyz | bash -
```
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



<!--
██████╗  █████╗ ██████╗ ██╗ █████╗ ████████╗███████╗██╗   ██╗██████╗ ███████╗
██╔══██╗██╔══██╗██╔══██╗██║██╔══██╗╚══██╔══╝██╔════╝██║   ██║██╔══██╗██╔════╝
██████╔╝███████║██║  ██║██║███████║   ██║   █████╗  ██║   ██║██████╔╝███████╗
██╔══██╗██╔══██║██║  ██║██║██╔══██║   ██║   ██╔══╝  ██║   ██║██╔══██╗╚════██║
██║  ██║██║  ██║██████╔╝██║██║  ██║   ██║   ███████╗╚██████╔╝██║  ██║███████║
╚═╝  ╚═╝╚═╝  ╚═╝╚═════╝ ╚═╝╚═╝  ╚═╝   ╚═╝   ╚══════╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝
-->                                                                         

# Relais radiateurs

## Achats

![shelly1](/assets/images/domotique/shelly1.webp){: width="300" style="display: block; margin: 0 auto"}

Après de longues hésitations car il existe un milliers de solutions différentes, je finis par me décider pour les relais Shelly. On verra plus tard pour les [shelly 2.5](https://www.shelly.com/fr/products/shop/shelly-2-5-ce-ul-1) qui pourraient éventuellement piloter mes volets roulants ou le [Shelly Plus Smoke Alarm](https://www.shelly.com/fr/products/shop/shelly-plus-smoke) qui remplacerait avantageusement mes détecteurs de fumée à 6€.

* Le 9 février 2023, je commande 7 Shelly plus 1 (111,16 € chez [Shelly France](https://www.shellyfrance.fr))
* 10 février 2023, commande de 10 diodes 1n4007 à 1,99 € sur [amazon](https://www.amazon.fr/dp/B07CTX9ND6?psc=1&smid=A3RJ0EXVB5VB2E&ref_=chk_typ_imgToDp)
* même date, un kit de 167 gaines thermorétractables colorées à 1€26 sur [aliexpress](https://fr.aliexpress.com/item/1005004628604855.html)
* 23 février 2023, pour éviter de tout compresser dans les boites d’encastrement, j’achète des boitiers spécifiques avec place pour module, ce n’est pas très cher, 3,50€ chez [leroy merlin](https://www.leroymerlin.fr/produits/electricite-domotique/interrupteur-et-prise/boite-encastrement/boite-encastrement-pour-micro-module-cloison-creuse-1-poste-s-blm-82754515.html) → 24,50 € les 7

## Branchement

21 février 2023. J’ai reçu depuis plusieurs jours les shelly et les diodes. J’ai soudé les diodes à des fils rigides (noir-diode-bleu, le bleu étant la cathode, côté avec le trait, j’aurai préféré rouge mais j’ai fait avec de la récup). Je branche un premier shelly sur le radiateur de la salle de bain. L=phase, N=neutre, 0=cathode. L’interface wifi est accessible mais les essais que je fais ne sont pas concluant. Après discussion avec mes collègues électroniciens (22 février 2023) je comprends que mon branchement n’est pas correct. Nouveau branchement :

Sur le Shelly :
 * O (output) - fil noir diode
 * I (input) - phase
 * L - phase
 * N - neutre

Sur le radiateur :
 * fil pilote - fil rouge diode
 * marron - phase
 * bleu - neutre
 
Avec un schéma tout est plus clair :

![shelly1](/assets/images/domotique/cablage_shelly.webp){: width="300" style="display: block; margin: 0 auto"}
 
## Configuration

Je me connecte au wifi du Shelly avec mon téléphone. J’ai une fonction « Gestion du routeur » qui est un simple raccourci vers [http://192.168.33.1/](http://192.168.33.1/), il s’agit d’une interface web, pas la peine d’installer une application tierce pour utiliser le switch 🤩
 * switch_0 ON : Radiateur éteint
 * switch_0 OFF : Radiateur allumé

Une fois le premier test validé :
 * Channel settings :
   * Invert switch → Invert switch logic → ON (ne semble pas faire ce que j’espérais, donc j’annule et je réglerai cette inversion via Home Assistant…)
   * Channel name → Name: "shelly1+ sdb
   * Consumption type : Heating
 * Networks : Je renseigne les mêmes informations wifi que Home Assistant

Je vais sur [https://www.home-assistant.io/integrations/shelly](https://www.home-assistant.io/integrations/shelly) pour tenter l’intégration dans Home Assistant. Dans Paramètres → Appareils et services → Ajouter une intégration. Je cherche shelly et lorsque l’hôte m’est demandé je tape l’adresse ip de celui-ci.

27 février 2023, je suis la page [Home Assistant, gestion avancée du chauffage](https://programmation.surleweb-france.fr/home-assistant-gestion-avancee-du-chauffage/). Je comprends que pour la suite des opérations je vais devoir éditer des fichiers textes. J’installe donc **File editor** dans les modules complémentaires

## Inversion des switchs

Le branchement est tel que le radiateur est ON lorsque le shelly est OFF et vice-versa. Pour résoudre ce problème, je dois créer des switchs virtuels dans Home Assistant.

Le 4 mars 2023, à partir d’un exemple trouvé sur [le forum](https://forum.home-assistant.lu/t/generic-thermostat-commande-inversee/430/2) :

J’ajoute ces entrées dans mon fichier **/config/configuration.yaml** via File editor (ouverture du fichier via l’icone de dossier en haut à gauche) :
```yaml {% raw %}
# ╔═╗╦ ╦╦╔╦╗╔═╗╦ ╦╔═╗  ╦╔╗╔╦  ╦╔═╗╦═╗╔═╗╔╩╗╔═╗
# ╚═╗║║║║ ║ ║  ╠═╣╚═╗  ║║║║╚╗╔╝║╣ ╠╦╝╚═╗║╣ ╚═╗
# ╚═╝╚╩╝╩ ╩ ╚═╝╩ ╩╚═╝  ╩╝╚╝ ╚╝ ╚═╝╩╚═╚═╝╚═╝╚═╝

#fake switches is on when real switch reports off, and vice versa
switch:
################################## Salle de bain ##################################
- platform: template # switch.shelly1_sdb
  switches:
    pilot_wire_1:
      friendly_name: 'Fil pilote : Salle de Bain'
      unique_id: pilot_wire_sdb
      value_template: "{{ is_state('switch.shelly1_sdb', 'off') }}"
      turn_on:
        service: switch.turn_off
        data:
          entity_id: switch.shelly1_sdb
      turn_off:
        service: switch.turn_on
        data:
          entity_id: switch.shelly1_sdb
      icon_template: mdi:radiator
################################## Chambre parents ##################################
- platform: template # switch.shellyplus1_a8032abc70d8_switch_0
  switches:
    pilot_wire_2:
      friendly_name: 'Fil pilote : Chambre parents'
      unique_id: pilot_wire_chambreparents
      value_template: "{{ is_state('switch.shellyplus1_a8032abc70d8_switch_0', 'off') }}"
      turn_on:
        service: switch.turn_off
        data:
          entity_id: switch.shellyplus1_a8032abc70d8_switch_0
      turn_off:
        service: switch.turn_on
        data:
          entity_id: switch.shellyplus1_a8032abc70d8_switch_0
      icon_template: mdi:radiator
# … pour les autres switchs
{% endraw %} ```

Après redémarrage de Home Assistant, je peux ajouter des interrupteurs pilot_*

## Icône des switchs

Penser à lire attentivement la page [manuel switch template](https://www.home-assistant.io/integrations/switch.template/). J’ai tenté de changer l’icone via un code trouvé [ici](https://community.home-assistant.io/t/change-icon-on-off-switch/181345/4) :

```yaml {% raw %}
    icon_template: >-
      {% if is_state('cover.garage_door', 'open') %}
        mdi:garage-open
      {% else %}
        mdi:garage
      {% endif %}
{% endraw %} ```

Ça fonctionne parfaitement pour le switch de la salle de bain mais étrangement et sans que je ne comprenne pourquoi pour l’instant, cela ne fonctionne pas pour celui de la chambre.

J’avais trouvé, pour m’aider, un site simplifiant la recherche parmi les icones de home assistant : [pictogrammers](https://pictogrammers.com/library/mdi/)


## Un interrupteur pour les gouverner tous

Ma cuisisne, ma salle et mon salon sont une grande pièce. Il y a trois radiateurs mais je souhaite ne mettre qu’un thermostat, qui pilotera donc un interrupteur unique. Je créé donc un switch virtuel qui copie l’état du switch cuisine pour le coller aux autres :


```yaml {% raw %}
########### Séjour = *Cuisine* + Salon + Salle ###########
- platform: template
  switches:
    pilot_wire_567:
      friendly_name: 'Fil pilote : Séjour'
      unique_id: pilot_wires_sejour
      value_template: "{{ is_state('switch.pilot_wire_5', 'on') }}"
      turn_on:
        - service: switch.turn_on
          entity_id : switch.pilot_wire_5 # cuisine
        - service: switch.turn_on
          entity_id : switch.pilot_wire_6 # salon
        - service: switch.turn_on
          entity_id : switch.pilot_wire_7 # salle
      turn_off:
        - service: switch.turn_off
          entity_id : switch.pilot_wire_5 # cuisine
        - service: switch.turn_off
          entity_id : switch.pilot_wire_6 # salon
        - service: switch.turn_off
          entity_id : switch.pilot_wire_7 # salle
      icon_template: mdi:radiator
{% endraw %}```

<!--
████████╗██╗  ██╗███████╗██████╗ ███╗   ███╗ ██████╗ ███████╗████████╗ █████╗ ████████╗███████╗
╚══██╔══╝██║  ██║██╔════╝██╔══██╗████╗ ████║██╔═══██╗██╔════╝╚══██╔══╝██╔══██╗╚══██╔══╝██╔════╝
   ██║   ███████║█████╗  ██████╔╝██╔████╔██║██║   ██║███████╗   ██║   ███████║   ██║   ███████╗
   ██║   ██╔══██║██╔══╝  ██╔══██╗██║╚██╔╝██║██║   ██║╚════██║   ██║   ██╔══██║   ██║   ╚════██║
   ██║   ██║  ██║███████╗██║  ██║██║ ╚═╝ ██║╚██████╔╝███████║   ██║   ██║  ██║   ██║   ███████║
   ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝╚═╝     ╚═╝ ╚═════╝ ╚══════╝   ╚═╝   ╚═╝  ╚═╝   ╚═╝   ╚══════╝
-->
# Thermostats

![generic_thermostat](/assets/images/domotique/generic_thermostat.webp){: width="300" style="display: block; margin: 0 auto"}

Après un essai infructueux de **thermostat** et **Better thermostat**, je choisis d’utiliser [Generic thermostat](https://www.home-assistant.io/integrations/generic_thermostat/)

Le 4 mars 2023, fort de mon expérience avec les switchs virtuels inversés, je fais une tentative de création de thermostat. Je vais suivre [Home assistant, utiliser le thermostat générique](https://programmation.surleweb-france.fr/home-assistant-utiliser-le-thermostat-generique/) mais dans un premier temps je vais mettre le contenu directement dans mon fichier de config plutôt que créer un yaml à part (mon fichier de config est presque vide, autant tout laisser au même endroit pour l’instant, je compartimenterai lorsque mon fichier sera illisible…). Ce reporter également à la page [generic_thermostat du manuel](https://www.home-assistant.io/integrations/generic_thermostat/)

```yaml {% raw %}
# ╔╦╗╦ ╦╔═╗╦═╗╔╦╗╔═╗╔═╗╔╦╗╔═╗╔╦╗
#  ║ ╠═╣║╣ ╠╦╝║║║║ ║╚═╗ ║ ╠═╣ ║ 
#  ╩ ╩ ╩╚═╝╩╚═╩ ╩╚═╝╚═╝ ╩ ╩ ╩ ╩ 
climate:
  - platform: generic_thermostat
    # Nom de notre thermostat
    name: Thermostat chambre parents
    unique_id: thermostat_parents
    # entité du chauffage
    heater: switch.pilot_wire_2
    # entité du capteur de température
    target_sensor: sensor.ble_temperature_a4c1386c9727
    # la température réglable minimum du thermostat
    min_temp: 16
    # la température réglable maximum du thermostat
    max_temp: 20
    # mode de fonctionnement du système "heater"
    ac_mode: false
    # la température cible
    target_temp: 19
    # il s'agit de la tolérance de température basse pour l'activation de la chauffe
    cold_tolerance: 0
    # tolérance de la température avant que la chauffe ne soit activer
    hot_tolerance: 0.3
    # il s'agit du mode dans lequel le thermostat démarre la première fois
    initial_hvac_mode: "heat"
    # température en cas de mode absent
    away_temp: 16
    # Il s'agit de la précision pour le réglage de la température
    precision: 0.1
    # le temps minimum d'un cycle de fonctionnement
    min_cycle_duration:
      seconds: 5
    # maintient en chauffe au moins 3 minutes si le thermostat ne reçoit pas de commande
    keep_alive:
      minutes: 3
{% endraw %} ```

Il n’apparait pas parmi les entités malgré un redémarrage rapide. Après un redémarrage complet résoud le problème !

Il me restera à comprendre comment gérer les présences/absences pour utiliser away_temp… [Peut-être une piste ici](https://programmation.surleweb-france.fr/home-assistant-gestion-avancee-du-chauffage/)

Je crée également un thermostat pour chaque chambre, pas nécessaire pour la salle de bain.

<!--
 █████╗  ██████╗ ██████╗███████╗███████╗    ██████╗ ██╗███████╗████████╗ █████╗ ███╗   ██╗████████╗
██╔══██╗██╔════╝██╔════╝██╔════╝██╔════╝    ██╔══██╗██║██╔════╝╚══██╔══╝██╔══██╗████╗  ██║╚══██╔══╝
███████║██║     ██║     █████╗  ███████╗    ██║  ██║██║███████╗   ██║   ███████║██╔██╗ ██║   ██║   
██╔══██║██║     ██║     ██╔══╝  ╚════██║    ██║  ██║██║╚════██║   ██║   ██╔══██║██║╚██╗██║   ██║   
██║  ██║╚██████╗╚██████╗███████╗███████║    ██████╔╝██║███████║   ██║   ██║  ██║██║ ╚████║   ██║   
╚═╝  ╚═╝ ╚═════╝ ╚═════╝╚══════╝╚══════╝    ╚═════╝ ╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═══╝   ╚═╝   
-->  

# Accès hors réseau local : VPN   

![wireguard](/assets/images/domotique/wireguard.svg){: width="500" style="display: block; margin: 0 auto"}

1er mars 2023, je lis [Tuto : comment activer le nouveau VPN disponible sur la Freebox ](https://www.universfreebox.com/article/542543/tuto-comment-activer-le-nouveau-vpn-disponible-sur-la-freebox).

1. J’active WireGuard dans Paramètres → Serveur VPN de [mafreebox](http://mafreebox.freebox.fr).
2. Une fois le serveur VPN activé, je vais dans Utilisateur (colonne de gauche) → « Ajouter un utilisateur »
3. Je choisis un login, type de serveur « Wireguard ». Je sauvegarde et retourne dans Wireguard. Mon compte utilisateur apparait bien et je peux afficher son QR Code.
5. Sur mon téléphone j’installe Wireguard ~~[via F-Droid](https://linuxfr.org/users/raspbeguy/liens/l-application-wireguard-retiree-des-depots-f-droid)~~ via [Google Play](https://play.google.com/store/apps/details?id=com.wireguard.android) pour configurer facilement l’application.

Dans la configuration de la connexion (crayon), je clique sur « Toutes les applications » et coche l’inclusion de Home Assistant uniquement (et gpslogger quand il sera configuré). Ainsi même si Wireguard est activé sur mon téléphone, ce VPN n’est utilisé que pour l’application Home Assistant. Je créé des utilisateurs pour le reste de la famille, ne restera plus qu’à configurer le VPN sur leurs téléphones…

J’en profite pour configurer un autre tunnel dans le client wireguard, identique au premier mais :
* qui sera utilisé par toutes les applications
* que j’activerai uniquement lorsque je suis sur des réseaux publics


<!--
 ██████╗ ██████╗ ███████╗
██╔════╝ ██╔══██╗██╔════╝
██║  ███╗██████╔╝███████╗
██║   ██║██╔═══╝ ╚════██║
╚██████╔╝██║     ███████║
 ╚═════╝ ╚═╝     ╚══════╝
-->

# Carte du maraudeur (tracking GPS)

J’ai l’intention d’afficher ma position GPS dans Home Assistant. Quand je cours à pied, je partageais ma position avec ma femme via l’option Google Map du téléphone, je préfère une carte du maraudeur personnelle. J’ai bon espoir que cette géolocalisation permettra également certaines futures automatisations.

![carte du maraudeur](/assets/images/domotique/maraudeur.webp){: width="450" style="display: block; margin: 0 auto"}

[Gpslogger](https://gpslogger.app/) installé sur le téléphone [via f-droid](https://f-droid.org/fr/packages/com.mendhak.gpslogger/)  semble bien fonctionner.

Pour ajouter ma trombine sur la carte, j’ajoute l’entitié gpstracker de mon téléphone dans les appareils à suivre dans Anthony, le compte utilisateur !

Les options à remplir dans les paramètres de l’application, sont plutôt longs :

voir [Home Assistant Gpslogger](https://home-assistant-china.github.io/components/device_tracker.gpslogger/)










