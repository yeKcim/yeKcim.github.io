---
layout: post
categories: ["Graphisme"]
date: 2016-02-19 14:45:00
title: "Post-it : Dégradé de couleur en fonction de la hauteur Blender Cycles"
---

Dans tout logiciel de mathématiques tel que ~~Matlab~~
[Gnuplot](http://www.gnuplot.info/),
[Matplotlib](http://matplotlib.org/) ou
[SageMath](http://www.sagemath.org/), on obtient
facilement des graphiques 3D dont la couleur varie en fonction de la
cote (l'axe z) mais dans Blender, ce n'est pas aussi automatique, il m'a
fallu pas mal chercher :

![blender_colorrampe_z_1](/assets/images/blender_colorrampe_z_1.webp)

\[[Source](http://blender.stackexchange.com/questions/5491/how-do-i-colour-a-3d-terrain-based-on-its-height)\]

J'avais déjà, dans un autre cas de figure, cherché à modifier la couleur
en fonction de la cote : à partir d'une image prise avec une caméra, je
souhaitais obtenir une courbe 3D représentant la luminosité. La cote
était alors automatiquement extraite de l'image, il suffisait d'utiliser
la même source pour la couleur :

![blender_colorrampe_z_2](/assets/images/blender_colorrampe_z_2.webp)

