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

template:
  - switch:
################################## Salle de bain ##################################
      - name: 'Fil pilote : Salle de Bain'
        unique_id: pilot_wire_sdb
        icon: mdi:radiator
        state: "{{ is_state('switch.shelly1_sdb', 'off') }}"
        turn_on:
          action: switch.turn_off
          target:
            entity_id: switch.shelly1_sdb
        turn_off:
          action: switch.turn_on
          target:
            entity_id: switch.shelly1_sdb

################################## Chambre Anthony ##################################
      - name: 'Fil pilote : Chambre Anthony'
        unique_id: pilot_wire_chambreanthony
        icon: mdi:radiator
        state: "{{ is_state('switch.shellyplus1_a8032abc70d8_switch_0', 'off') }}"
        turn_on:
          action: switch.turn_off
          target:
            entity_id: switch.shellyplus1_a8032abc70d8_switch_0
        turn_off:
          action: switch.turn_on
          target:
            entity_id: switch.shellyplus1_a8032abc70d8_switch_0

################################## Chambre Owen ##################################
      - name: 'Fil pilote : Chambre Owen'
        unique_id: pilot_wire_chambreowen
        icon: mdi:radiator
        state: "{{ is_state('switch.shelly1_chambre_owen', 'off') }}"
        turn_on:
          action: switch.turn_off
          target:
            entity_id: switch.shelly1_chambre_owen
        turn_off:
          action: switch.turn_on
          target:
            entity_id: switch.shelly1_chambre_owen

################################## Chambre Yaël ##################################
      - name: 'Fil pilote : Chambre Yaël'
        unique_id: pilot_wire_chambreyael
        icon: mdi:radiator
        state: "{{ is_state('switch.shelly1_chambre_yael_switch_0', 'off') }}"
        turn_on:
          action: switch.turn_off
          target:
            entity_id: switch.shelly1_chambre_yael_switch_0
        turn_off:
          action: switch.turn_on
          target:
            entity_id: switch.shelly1_chambre_yael_switch_0

################################## Cuisine ##################################
      - name: 'Fil pilote : Cuisine'
        unique_id: pilot_wire_cuisine
        icon: mdi:radiator
        state: "{{ is_state('switch.shellyplus1_a8032abc7fc8_switch_0', 'off') }}"
        turn_on:
          action: switch.turn_off
          target:
            entity_id: switch.shellyplus1_a8032abc7fc8_switch_0
        turn_off:
          action: switch.turn_on
          target:
            entity_id: switch.shellyplus1_a8032abc7fc8_switch_0

################################## Salon ##################################
      - name: 'Fil pilote : Salon'
        unique_id: pilot_wire_salon
        icon: mdi:radiator
        state: "{{ is_state('switch.shellyplus1_a8032abe7cb4_switch_0', 'off') }}"
        turn_on:
          action: switch.turn_off
          target:
            entity_id: switch.shellyplus1_a8032abe7cb4_switch_0
        turn_off:
          action: switch.turn_on
          target:
            entity_id: switch.shellyplus1_a8032abe7cb4_switch_0

################################## Salle ##################################
      - name: 'Fil pilote : Salle'
        unique_id: pilot_wire_salle
        icon: mdi:radiator
        state: "{{ is_state('switch.shellyplus1_a8032abc5f84_switch_0', 'off') }}"
        turn_on:
          action: switch.turn_off
          target:
            entity_id: switch.shellyplus1_a8032abc5f84_switch_0
        turn_off:
          action: switch.turn_on
          target:
            entity_id: switch.shellyplus1_a8032abc5f84_switch_0

################################## Séjour = *Cuisine* + Salon + Salle ##################################
      - name: 'Fil pilote : Séjour'
        unique_id: pilot_wires_sejour
        icon: mdi:radiator
        state: "{{ is_state('switch.pilot_wire_5', 'on') }}"
        turn_on:
          - action: switch.turn_on
            target:
              entity_id: switch.pilot_wire_5 # cuisine
          - action: switch.turn_on
            target:
              entity_id: switch.pilot_wire_6 # salon
          - action: switch.turn_on
            target:
              entity_id: switch.pilot_wire_7 # salle
        turn_off:
          - action: switch.turn_off
            target:
              entity_id: switch.pilot_wire_5 # cuisine
          - action: switch.turn_off
            target:
              entity_id: switch.pilot_wire_6 # salon
          - action: switch.turn_off
            target:
              entity_id: switch.pilot_wire_7 # salle
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
██████╗ ██╗      █████╗ ███╗   ██╗██╗███████╗██╗ ██████╗ █████╗ ████████╗███████╗██╗   ██╗██████╗ 
██╔══██╗██║     ██╔══██╗████╗  ██║██║██╔════╝██║██╔════╝██╔══██╗╚══██╔══╝██╔════╝██║   ██║██╔══██╗
██████╔╝██║     ███████║██╔██╗ ██║██║█████╗  ██║██║     ███████║   ██║   █████╗  ██║   ██║██████╔╝
██╔═══╝ ██║     ██╔══██║██║╚██╗██║██║██╔══╝  ██║██║     ██╔══██║   ██║   ██╔══╝  ██║   ██║██╔══██╗
██║     ███████╗██║  ██║██║ ╚████║██║██║     ██║╚██████╗██║  ██║   ██║   ███████╗╚██████╔╝██║  ██║
╚═╝     ╚══════╝╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝╚═╝     ╚═╝ ╚═════╝╚═╝  ╚═╝   ╚═╝   ╚══════╝ ╚═════╝ ╚═╝  ╚═╝
-->

# Planificateur

![planificateur](/assets/images/domotique/planificateur.webp){: width="450" style="display: block; margin: 0 auto"}

5 mars 2023, j’en suis à trois radiateurs configurés dans Home Assistant, avec 2 thermostats fonctionnels (pas la peine dans la salle de bain) et avant d’installer les autres, je pense qu’il est urgent de regarder comment se gère le planning.

Je trouve deux options :
 * Paramètres → Appareils et services → Entrées → Créer une entrée → [Planification](https://www.home-assistant.io/integrations/schedule/)
 * [Scheduler component](https://github.com/nielsfaber/scheduler-component) et [Scheduler card](https://github.com/nielsfaber/scheduler-card)

Dans un premier temps, j’utilise [Scheduler component](https://github.com/nielsfaber/scheduler-component), il me permet de définir les températures en fonction d’horaires.

## Installation 

 * Installation de Scheduler component : HACS → Intégration → Scheduler component
 * Intégration de Scheduler component : Paramètres → Intégrations et services → + Ajouter une intégration → Scheduler
 * Installation de Scheduler card (GUI) : HACS → Interface → Scheduler-card

Je peux maintenant ajouter une carte Scheduler. Pour le premier essai, je crée un planification que j’applique la semaine et un autre pour le week-end. Reste à voir si ça fonctionne bien. Pour l’instant, 6 mars 2023, cette solution me convient.

## Affaire à suivre…

Ce n’est pas idéal car je ne sais pas encore trop comment l’intégrer à une gestion présence/absence et je n’utilise finalement pas la fonction away_temp du thermostat mais dans un premier temps ça répond à mon besoin initial de base… (via un simple bouton présent/absent ? mais comment ce bouton sera-t-il pris en compte ? [À voir](https://forum.hacf.fr/t/gestion-de-bout-en-bout-du-chauffage/4897/176).

À lire :
 * [Planification](https://www.home-assistant.io/integrations/schedule/)
 * Alternative à voir : [Sheddy](https://canaletto.fr/post/home-assistant-and-schedy-encore) ? avec l’[automation](https://community.home-assistant.io/t/set-the-temperature-of-the-generic-thermostat-with-a-automation/467823) ?
 * [Home Assistant Climate Scheduler](https://github.com/FrancisLab/hass-climate-scheduler) ?
 * la [gestion des zones](https://github.com/nielsfaber/zoned-heating) ?
 * [https://johanf85.github.io/home-assistant-heating-configuration/description.html](https://johanf85.github.io/home-assistant-heating-configuration/description.html)
 * [https://ledstripsandcode.blogspot.com/2018/11/simple-thermostat-scheduler-in-home.html](https://ledstripsandcode.blogspot.com/2018/11/simple-thermostat-scheduler-in-home.html)
 * [https://www.home-assistant.io/integrations/schedule/#services](https://www.home-assistant.io/integrations/schedule/#services)
 * [https://smarthomescene.com/guides/how-to-create-schedules-in-home-assistant/](https://smarthomescene.com/guides/how-to-create-schedules-in-home-assistant/)
 * [https://canaletto.fr/post/home-assistant-planification-encore](https://canaletto.fr/post/home-assistant-planification-encore)
 * [https://canaletto.fr/post/home-assistant-and-planification-la-suite](https://canaletto.fr/post/home-assistant-and-planification-la-suite)
 * [https://github.com/custom-components/climate.programmable_thermostat](https://github.com/custom-components/climate.programmable_thermostat)

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

J’ai quelques temps utilisé [Gpslogger](https://gpslogger.app/) mais en 2026, il y a directement la localisation disponible dans Home assistant companion, à tester…


<!--
███████╗███╗   ███╗ ██████╗ ██╗  ██╗███████╗
██╔════╝████╗ ████║██╔═══██╗██║ ██╔╝██╔════╝
███████╗██╔████╔██║██║   ██║█████╔╝ █████╗  
╚════██║██║╚██╔╝██║██║   ██║██╔═██╗ ██╔══╝  
███████║██║ ╚═╝ ██║╚██████╔╝██║  ██╗███████╗
╚══════╝╚═╝     ╚═╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝
-->

# Shelly Smoke

30 novembre 2023, j’ai reçu 2 détecteur de fumée Shelly Smoke. La [documentation](https://www.home-assistant.io/integrations/shelly), [l’aide complémentaire](https://github.com/home-assistant/core/issues/89228).

![Shelly Smoke](/assets/images/domotique/smoke.webp){: width="450" style="display: block; margin: 0 auto"}

* J’enlève la protection de la pile, le détecteur s’allume alors automatiquement
* J’appuie 3 fois rapidement sur le bouton pour activer le mode configuration pendant 2 minutes
* Sur mon téléphone je me connecte alors au wifi ShellyPlusSmoke-xxxFC (pour le séjour) et ShellyPlusSmoke-xxx18 (pour les chambres)
* "Gérer le routeur" ou http://192.168.33.1/ pour :
  * Configurer le wifi
  * Settings → Outbound websocket settings :
    * Enable Outbound Websocket
    * Connection type : TLS no validation
    * Serveur : ws://192.168.0.41:8123/api/shelly/ws

Après "Save settings" , je valide le reboot.

Une fois cette étape faite, les shelly-smoke apparaissent dans les intégrations, avec leurs entitées !

Je défini des IP fixes pour ces deux entrées dans la config du DHCP de la freebox, au cas où, pour retrouver plus facilement leurs interfaces de configuration.

![Shelly Smoke dans HAOS](/assets/images/domotique/smoke_carte.webp){: style="display: block; margin: 0 auto"}

Reste à voir comment lancer une alerte sur mon téléphone en cas de détection de fumée ou comment lui dire de se mettre en pause si je fais un essai de fumigène dans la maison. Si j’avais des ampoules connectées, je pourrais automatiquement allumé les lumières la nuit en cas d’incendie pour faciliter une évacuation.

 
<!-- 
██╗   ██╗ ██████╗ ██╗     ███████╗████████╗███████╗      ██████╗  ██████╗ ██╗   ██╗██╗      █████╗ ███╗   ██╗████████╗███████╗
██║   ██║██╔═══██╗██║     ██╔════╝╚══██╔══╝██╔════╝      ██╔══██╗██╔═══██╗██║   ██║██║     ██╔══██╗████╗  ██║╚══██╔══╝██╔════╝
██║   ██║██║   ██║██║     █████╗     ██║   ███████╗      ██████╔╝██║   ██║██║   ██║██║     ███████║██╔██╗ ██║   ██║   ███████╗
╚██╗ ██╔╝██║   ██║██║     ██╔══╝     ██║   ╚════██║      ██╔══██╗██║   ██║██║   ██║██║     ██╔══██║██║╚██╗██║   ██║   ╚════██║
 ╚████╔╝ ╚██████╔╝███████╗███████╗   ██║   ███████║      ██║  ██║╚██████╔╝╚██████╔╝███████╗██║  ██║██║ ╚████║   ██║   ███████║
  ╚═══╝   ╚═════╝ ╚══════╝╚══════╝   ╚═╝   ╚══════╝      ╚═╝  ╚═╝ ╚═════╝  ╚═════╝ ╚══════╝╚═╝  ╚═╝╚═╝  ╚═══╝   ╚═╝   ╚══════╝
-->

# Volets roulants

Janvier 2025, je domotise mes volets motorisés. J’achète 6 Shelly+2PM. 

![shelly+2](/assets/images/domotique/shelly+2pm.webp){: width="300" style="display: block; margin: 0 auto"}

## Branchement 

![shelly2](/assets/images/domotique/cablage_shelly2.webp){: width="550" style="display: block; margin: 0 auto"}

Une fois branché, je me connecte à son wifi, dans mon navigateur : http://192.168.33.1

## Configuration

Dans la configuration :
 * je définis le wifi (si le wifi défini et connecté, il est possible de configurer le module depuis n’importe quel pc/phone du réseau en tapant l’IP)
 * Settings → Authentication : Password protected device ("Shelly+Pass23")
 * Settings → Device profile cover
 * Settings → Device Name : "Volet Salon"…
 * Settings → Firmware update 
 * Général settings : Calibration
 * Enable obstacle detection

Si les boutons sont inversés :
 * Cover input settings → Enable swap inputs

## Automatisation

Je veux que les volets s’ouvrent automatiquement le matin mais à des horaires différents en semaine et les week-ends. Pour cela j’ai besoin de [Workday](https://www.home-assistant.io/integrations/workday) :

 * Paramètres → Appareils et services → Ajouter une intégration : Jour de travail (France)

Dans les automatisations :
 * Ouvrir les volets à 7h les jours de travail
 * Ouvrir les volets à 8h45 les week-end et jours fériés
 * Fermer les volets au coucher du soleil (+ 20 minutes)

![automatisation volets](/assets/images/domotique/volets_auto.webp){: width="550" style="display: block; margin: 0 auto"}

J’ajoute aussi un bouton pour activer/désactiver les automatisations des volets et des boutons pour ouvrir/fermer tous les volets.

Peut-être qu’à terme je devrai également penser à :
 * utiliser le calendrier pour activer/désactiver en fonction d’entrées "congés"…
 * ajouter un compte à rebours avant la prochaine ouverture/fermeture automatique
 * l’été, fermer les volets en fonction de la température et la météo ?

## Détection ouverture porte fenêtre

Dernier point : je sors parfois par la porte fenêtre, il me faut donc un détecteur Shelly BLU Door/Window : Si la porte fenêtre n’est pas fermée
Fermer automatiquement mais pour la porte fenêtre de la salle, si ouverte ne pas fermer, détecteur à ajouter…

Le Shelly BLU Door/Window est directement détecté par Home Assistant (une fois la pile insérée) via le protocole BTHome. Il faut placer l’aimant de façon à ce qu’il soit pile à la position entre ouvert/fermé afin qu’un tout petit décalage valide l’ouverture. Je choisis de mettre l’aimant sur le montant, au dessus de la porte fenêtre et le détecteur en haut, proche du milieu (une ouverture même minime implique ici un plus gros écart) 

Dans l’automatisation j’ajoute une condition sur l’état du détecteur pour fermer le volet de la salle :

```yaml {% raw %}
alias: "Volets : fermer au coucher du soleil"
description: ""
triggers:
  - trigger: sun
    event: sunset
    offset: "00:20:00"
conditions: []
actions:
  - action: cover.close_cover
    metadata: {}
    data: {}
    target:
      entity_id:
        - cover.chambre3
        - cover.cuisine
        - cover.salon
        - cover.chambre1
        - cover.chambre2
  - if:
      - condition: state
        entity_id: binary_sensor.bthome_sensor_2fad_window
        state: "off"
    then:
      - action: cover.close_cover
        metadata: {}
        data: {}
        target:
          entity_id: cover.salle
    else:
      - wait_for_trigger:
          - trigger: state
            entity_id:
              - binary_sensor.bthome_sensor_2fad_window
            from: "on"
            to: "off"
            for:
              hours: 1
              minutes: 0
              seconds: 0
      - action: cover.close_cover
        metadata: {}
        data: {}
        target:
          entity_id: cover.volet_salle_cover_0
mode: single
{% endraw %} ```


# Mises à jour, BLE et HACS

Été 2025, suite à différentes mises à jour, la température n’est plus relevable dans mon instance. Pour récupérer l’information, je dois mettre à jour Passive BLE et pour cela, la mise à jour de HACS doit être forcée en version 2. J’applique [les conseils trouvé sur la toile](https://www.hacf.fr/hacs_installation_utilisation/), en particulier :
```sh
wget -O - https://get.hacs.xyz | bash -
```
Une fois HACS à jour, la mise à jour de BLE (et plusieurs autre plugins) est possible et la température est à nouveau disponible !


<!--                      ███
 ██████╗ █████╗ ███████╗███████╗    ████████╗ █████╗ ██████╗  ██████╗ 
██╔════╝██╔══██╗██╔════╝██╔════╝    ╚══██╔══╝██╔══██╗██╔══██╗██╔═══██╗
██║     ███████║█████╗  █████╗         ██║   ███████║██████╔╝██║   ██║
██║     ██╔══██║██╔══╝  ██╔══╝         ██║   ██╔══██║██╔═══╝ ██║   ██║
╚██████╗██║  ██║██║     ███████╗       ██║   ██║  ██║██║     ╚██████╔╝
 ╚═════╝╚═╝  ╚═╝╚═╝     ╚══════╝       ╚═╝   ╚═╝  ╚═╝╚═╝      ╚═════╝ 
-->    
     
# Prise connectée Tapo

J’ai acheté dans la précipitation, une prise connectée Tapo P110. L’intégration passe par HACS, nécessite des ajustemzents, il est nécessaire d’installer l’app du fabricant sur le téléphone, donc évidemment, si je pouvais je changerais pour une autre marque. Mais maintenant que je l’ai…

* Installation de l’application Tapo via Playstore
* Configuration de la prise P110 sur le wifi
* Dans l’app : Moi → Services tiers → Compatibilité tierce : Activé (Sans cette étape l’authentification ne sera pas possible)
* HACS : Paramètres → Appareils et services → + Ajouter une intégration → TP Link Tapo

Une cafetière est branchée dessus. Je veux un moyen de programmer la cafetière une fois, pour qu’il soit prêt à être bu à l’heure que j’indique. Ce bouton se désactive, il faudra que je reclique sur le bouton pour relancer. J’ai besoin d’un texte qui m’indique l’état de la cafetière. Pour gérer cela, j’ai utilisé différentes IA. Après plusieurs essais, modifications, principalement dans Claude (les autres IA ont de bonnes idées mais Claude était le seul à garder le code réellement fonctionnel.

![automatisation café](/assets/images/domotique/cafe.webp){: width="550" style="display: block; margin: 0 auto"}

```yaml {% raw %}
########### configuration.yaml ########### 
input_datetime:
  cafe_pret:
    name: "Café prêt à"
    has_time: true
    has_date: false
  cafe_activation:
    name: "Activation cafetière"
    has_time: true
    has_date: true
  cafe_extinction:
    name: "Extinction cafetière"
    has_time: true
    has_date: true

input_boolean:
  cafe_demain:
    name: "Je veux un café"
    icon: mdi:coffee

input_number:
  cafe_duree_chauffe:
    name: "Durée de chauffe"
    min: 5
    max: 60
    step: 5
    initial: 10
    unit_of_measurement: min
    icon: mdi:fire
  cafe_duree_repos:
    name: "Durée de repos"
    min: 0
    max: 60
    step: 5
    initial: 15
    unit_of_measurement: min
    icon: mdi:coffee-outline
{% endraw %} ```

```yaml {% raw %}
########### automations.yaml ########### 
- alias: "Cafetière - Calcul heures activation et extinction"
  trigger:
    - platform: state
      entity_id: input_boolean.cafe_demain
      to: "on"
  action:
    - service: input_datetime.set_datetime
      target:
        entity_id: input_datetime.cafe_activation
      data:
        datetime: >
          {% set pret = states('input_datetime.cafe_pret')[0:5] %}
          {% set chauffe = states('input_number.cafe_duree_chauffe') | int %}
          {% set repos = states('input_number.cafe_duree_repos') | int %}
          {% set activation = today_at(pret) - timedelta(minutes=chauffe + repos) %}
          {% if activation < now() %}
            {{ (activation + timedelta(days=1)).strftime('%Y-%m-%d %H:%M:%S') }}
          {% else %}
            {{ activation.strftime('%Y-%m-%d %H:%M:%S') }}
          {% endif %}
    - service: input_datetime.set_datetime
      target:
        entity_id: input_datetime.cafe_extinction
      data:
        datetime: >
          {% set pret = states('input_datetime.cafe_pret')[0:5] %}
          {% set repos = states('input_number.cafe_duree_repos') | int %}
          {% set extinction = today_at(pret) - timedelta(minutes=repos) %}
          {% if extinction < now() %}
            {{ (extinction + timedelta(days=1)).strftime('%Y-%m-%d %H:%M:%S') }}
          {% else %}
            {{ extinction.strftime('%Y-%m-%d %H:%M:%S') }}
          {% endif %}
  mode: single

- alias: "Cafetière - Allumage"
  trigger:
    - platform: time
      at: input_datetime.cafe_activation
  condition:
    - condition: state
      entity_id: input_boolean.cafe_demain
      state: "on"
  action:
    - service: switch.turn_on
      target:
        entity_id: switch.prise_connectee_tapo
  mode: single

- alias: "Cafetière - Extinction"
  trigger:
    - platform: time
      at: input_datetime.cafe_extinction
  condition:
    - condition: state
      entity_id: input_boolean.cafe_demain
      state: "on"
  action:
    - service: switch.turn_off
      target:
        entity_id: switch.prise_connectee_tapo
    - service: input_boolean.turn_off
      target:
        entity_id: input_boolean.cafe_demain
  mode: single
{% endraw %} ```

```yaml {% raw %}
########### Carte Lovelace ########### 
type: vertical-stack
cards:
  - type: markdown
    content: >
      ## ☕ Cafetière

      {% set pret = states('input_datetime.cafe_pret')[0:5] %}

      {% set chauffe = states('input_number.cafe_duree_chauffe') | int %}

      {% set repos = states('input_number.cafe_duree_repos') | int %}

      {% set activation = state_attr('input_datetime.cafe_activation',
      'timestamp') | as_datetime | as_local %}

      {% if is_state('switch.prise_connectee_tapo', 'on') and
      is_state('input_boolean.cafe_demain', 'on') %}

      🔥 En chauffe — prête à {{ pret }}

      {% elif is_state('input_boolean.cafe_demain', 'on') %}

      {% set delta = (activation - now()).total_seconds() %}

      {% set h = (delta // 3600) | int %}

      {% set m = ((delta % 3600) // 60) | int %}

      🟢 Café prêt à {{ pret }}

      🔌 Activation dans {% if delta < 60 %}moins d'une minute{% elif h > 0 %}{{
      h }}h {{ m }} min{% else %}{{ m }} min{% endif %} (à {{
      activation.strftime('%H:%M') }})

      ⏱ Chauffe {{ chauffe }} min · Repos {{ repos }} min

      {% else %}

      ⚪ Aucune activation programmée

      {% endif %}
  - type: entities
    entities:
      - entity: input_datetime.cafe_pret
        name: Café prêt à
      - entity: input_number.cafe_duree_chauffe
        name: Durée de chauffe
      - entity: input_number.cafe_duree_repos
        name: Durée de repos
      - entity: input_boolean.cafe_demain
        name: Je veux un café
        icon: mdi:coffee


{% endraw %} ```

<!--  
 █████╗ ███████╗██████╗ ██╗██████╗  █████╗ ████████╗███████╗██╗   ██╗██████╗
██╔══██╗██╔════╝██╔══██╗██║██╔══██╗██╔══██╗╚══██╔══╝██╔════╝██║   ██║██╔══██╗
███████║███████╗██████╔╝██║██████╔╝███████║   ██║   █████╗  ██║   ██║██████╔╝
██╔══██║╚════██║██╔═══╝ ██║██╔══██╗██╔══██║   ██║   ██╔══╝  ██║   ██║██╔══██╗
██║  ██║███████║██║     ██║██║  ██║██║  ██║   ██║   ███████╗╚██████╔╝██║  ██║
╚═╝  ╚═╝╚══════╝╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝   ╚══════╝ ╚═════╝ ╚═╝  ╚═╝
-->

# Aspirateur

J’ai un aspirateur iRobot, pour l’instant j’ai peu d’automatisation. Je prévois à terme d’automatiser l’aspiration lorsque personne n’est à la maison (détection via les téléphones), mettre en pause en cas d’appel téléphonique,…). Mais je peux dans un premier temps au moins améliorer la carte de base :

![carte aspirateur](/assets/images/domotique/aspi.webp){: width="550" style="display: block; margin: 0 auto"}

```yaml {% raw %}
########### Carte Lovelace ########### 
type: vertical-stack
cards:
  - type: markdown
    content: |
      ## 🤖 Wall-E
      {% set state = states('vacuum.wall_e') %}
      {% if state == 'cleaning' %}
      🟢 Aspiration en cours
      {% elif state == 'docked' %}
      🔵 En charge · Batterie {{ states('sensor.wall_e_battery_level') }}%
      {% elif state == 'returning' %}
      🔄 Retour à la base…
      {% elif state == 'paused' %}
      ⏸️ En pause
      {% elif state == 'error' %}
      🔴 Erreur : {{ state_attr('vacuum.wall_e', 'error') }}
      {% else %}
      ⚪ En attente
      {% endif %}
      {% if is_state('input_boolean.walle_programme', 'on') %}
      ⏰ Programmé pour {{ states('input_datetime.irobot_schedule')[0:5] }}
      {% endif %}
      {% if is_state('binary_sensor.wall_e_bin_full', 'on') %}
      ⚠️ Bac plein — pensez à le vider
      {% endif %}
  - type: entities
    entities:
      - entity: vacuum.wall_e
        name: Wall-E
      - type: button
        name: Aspire maintenant
        icon: mdi:play-circle
        tap_action:
          action: call-service
          service: vacuum.start
          target:
            entity_id: vacuum.wall_e
      - entity: input_datetime.irobot_schedule
        name: Aspire à
      - entity: input_boolean.walle_programme
        name: Activer la programmation
        icon: mdi:clock-check
      - type: button
        name: Pause — retour à la base
        icon: mdi:stop-circle
        tap_action:
          action: call-service
          service: vacuum.return_to_base
          target:
            entity_id: vacuum.wall_e
{% endraw %} ```

Pour pouvoir l’utiliser, je dois ajouter un bout de code à la fin de automations.yaml :

```yaml {% raw %}
- id: 'walle_aspiration_programmee'
  alias: "Wall-E - Aspiration programmée"
  triggers:
  - trigger: time
    at: input_datetime.irobot_schedule
  conditions:
  - condition: state
    entity_id: input_boolean.walle_programme
    state: "on"
  actions:
  - action: vacuum.start
    target:
      entity_id: vacuum.wall_e
  - action: input_boolean.turn_off
    target:
      entity_id: input_boolean.walle_programme
  mode: single
{% endraw %} ```


et insérer irobot_auto… dans input_boolean de configuration.yaml :

```yaml {% raw %}
input_boolean:
  cafe_demain:
    name: "Je veux un café"
    icon: mdi:coffee
  walle_programme:
    name: "Wall-E programmé"
    icon: mdi:clock-outline
{% endraw %} ```



# À voir…

* J’essaye Strava via HACS… mais nécessite une url publique, j’aurais aiméé ajouté beacon automatiquement sur la carte
* Je peux accéder à Home Assistant via l’interface web. Dedans, je peux "Ouvrir l’interface utilisateur web" de "Terminal & SSH" pour avoir accès en ssh mais quand je tente un ssh directement depuis un terminal de mon ordinateur ça ne fonctionne pas
* Ma carte du maraudeur ne fonctionne pas pour l’instant (surtout que je n’ai plus wireguard depuis que je suis parti de chez free
* Les automatisations de l’aspirateur serait vraiment génial
* Je rêve que mon radio-réveil lampe s’intègre bien mieux dans home assistant
* Il va falloir acheter des prises connectées pour gérer les décorations de noël, si possible du shelly pas du tapo…
* Si j’avais des détecteurs d’ouverture de porte sur chaque porte-fenêtre, je pourrais mettre le chauffage en pause ou me faire un petit système d’alarme
* …



