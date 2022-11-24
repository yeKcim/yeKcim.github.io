---
layout: post
categories: ["Graphisme"]
date: 2016-07-03 17:05:00
title: "Post-it Inkscape : Réinitialiser le centre de rotation"
---

Ce matin, j’ai eu le plaisir d’assister à quelques conférences de Grafik Labor,
événement proposé par l’AFGRAL, dont l’objectif est de fédérer autour des logiciels
libres graphiques : des conférences Gimp, Blender, Inkscape, Scribus,
Synfig, Gstreamer,… pour moi c’est un peu le paradis. Ça se déroulait
le 2 et 3 juillet à Rennes et les locaux d’[activdesign](https://activdesign.eu/) étaient complets, c’est vraiment
cool de voir que le sujet intéresse plein de monde.

Ce matin, Elisa de C. Guerra présentait les bases de Inkscape. Je
connais déjà assez bien ce soft puisque j’initie moi-même régulièrement
mes collègues à l’utilisation de ce logiciel de dessin vectoriel. La
conférence était donc très intéressante pour moi, non pas pour apprendre
les bases mais pour voir comment Elisa, que je sais très bonne
pédagogue, développe sa présentation, pour éventuellement m’en inspirer
pour la forme, le rythme ou le contenu.

Une question s’est posée : Comment réinitialiser la position du centre
de rotation ? C’est une question que je m’étais déjà posée sans jamais
être suffisamment ennuyé pour chercher à la résoudre.

## Quel est le problème ?

Lorsque vous cliquez deux fois avec l’outil de sélection sur un objet,
vous faites apparaître les poignées de rotation et de cisaillement. Au
centre de l’objet apparaît une croix : le centre de rotation.

![reinitcentrerot_1](/assets/images/inkscape-reinitcentrerot_1.webp)

Il est possible de déplacer cette croix pour personnaliser l’axe de
rotation mais comment faire pour replacer ce centre de rotation
parfaitement au centre de l’objet si on l’a préalablement bougé ?

## Quelles solutions ?

Une solution très simple proposée par un membre de l’assistance, ce
matin, m’a intriguée et j’ai donc tenté de trouver une solution plus
"correcte". Voici toutes les solutions que j’ai identifiées (la
première est celle proposée, les deux autres sont celles que je viens de
trouver, en bidouillant lors de la rédaction ce billet) :

-   Sélectionner l’objet et le grouper (Ctrl+G). Même si l’objet n’est
    groupé qu’à lui même, le centre de rotation n’est plus celui de
    l’objet mais celui du groupe, par défaut au centre donc… Ceci à
    l’avantage de permettre de réinitialiser le centre de rotation sans
    perdre définitivement le centre de rotation personnalisé.
-   Sélectionner l’objet et afficher l’éditeur XML (Maj+Ctrl+X),
    redéfinir à 0 les valeurs de **inskscape:transform-center-x** et
    **inskscape:transform-center-y**

![reinitcentrerot_2](/assets/images/inkscape-reinitcentrerot_2.webp)

-   Plus simplement : Shift+clic gauche sur la croix (amusant de
    constater finalement qu’une solution très simple est disponible)

