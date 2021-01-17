---
layout: post
title: "Effet carousel via jQuery"
date: "2008-12-29"
categories: 
  - "web"
tags: 
  - "browser"
  - "css"
  - "framework"
  - "html"
  - "javascript"
  - "jquery"
  - "plugin"
  - "simplecarrousel"
---

Ces derniers temps je me suis mis à bidouiller des scripts en me basant sur jQuery. Je vous présente le premier fruit de ce bidouillage : `simpleCarousel`. Ce plugin permet très simplement de mettre en place un effet carrousel sur une liste d'image. Ce script utilise du HTML, relevé à l'aide d'une pincée de CSS, le tout saupoudré d'une bonne dose de javascript via l'utilisation de jQuery.

1°) le HTML. très simplement on utilisera un balise `div` auquel on assigne un attribut `id` unique. Cette balise va contenir une liste non-ordonnée d'image sur laquelle l'effet carousel sera appliquée. Ensuite on termine, par ajouter dans la page les balises qui serviront à faire bouger vers la droite ou vers la gauche le carrousel. _A noter que l'on peut ajouter autant de bouton de navigation que l'on veut vue que le script va cibler l' attribut `class` des balises et non un `id` particulier._ Et c'est tout pour le HTML vous devriez avoir un code source HTML de ce type: \[sourcecode language="html"\]

- ![](/path/to/my/images "titre de l'image 1")
- ![](/path/to/my/images "titre de l'image 2")
- ![](/path/to/my/images "titre de l'image 3")
- ![](/path/to/my/images "titre de l'image 4")

« précédent | suivant »

\[/sourcecode\]

2°) Maintenant on ajoute le CSS qui va bien. Le script va généré automatiquement l'ajout d'un titre à chaque image correspondant à la valeur de l'attribut `title` de l'image si celle-ci en possède un. Le titre sera compris dans une balise `em` qui suivra directement l'image utilisée pour la générer. En utilisant le CSS on pourra mettre en valeur ce titre et également, par exemple, ajouter un effet lorsque l'on survole une image et pourquoi pas mettre en évidence les balises de navigation, ce qui peut donner par exemple : \[sourcecode language="css"\]#id\_unique li img { border:2px solid #fff; } #id\_unique li:hover img { border:2px solid #fb6f3a; } #id\_unique li em { display:block; text-align:center; } #id\_unique li:hover em { color:#fb6f3a; } .move-left, .move-right { background:transparent; color:#fb6f3a; cursor:pointer; } \[/sourcecode\]

3°) Lorsque tout est près, on complète le tableau avec l'ajout du Javascript via jQuery. On charge `jQuery` et mon plugin `simpleCarousel` : \[sourcecode language="javascript"\]

<script type="text/javascript" src="/path/to/jquery.js?v=1.26"></script>

 

<script type="text/javascript" src="/path/to/simpleCarousel.js"></script>

<script type="text/javascript">jQuery(function($) { var params = {'imgWidth' : 160, 'btnLeft' : 'move-left', 'btnRight' : 'move-right', 'nbViewItems' : 2, 'nbScrollItems' : 2, 'speed' : 1500 }; $('#onepiece').simpleCarousel(params); }); </script>

 \[/sourcecode\]

Les paramètres sont assez simples et intuitifs _(du moins je l'espère)_ :

- `imgWidth` : la taille en pixel  de la largeur des images ;
- `btnLeft` : la classe de l'élément qui va permettre le défilement de l'animation vers la gauche ;
- `btnRight` : la classe de l'élément qui va permettre le défilement de l'animation vers la droite ;
- `nbViewItems` : nombre d'items à montrer;
- `nbScrollItems` : nombre d'items que l'on va faire défiler ;
- `speed` : détermine la vitesse de défilement (exprimée en millisecondes);

Et voila ce qu'il fallait démontrer et comme un exemple vaut mieux que 10000 lignes d'explication, voici [simpleCarousel en action](http://nyamsprod.com/test/carrousel/new.html "Exemple d'utilisation de simpleCarrousel").

télécharger [simpleCarousel](http://nyamsprod.com/test/carrousel/jquery.simpleCarousel.js "le plugin jQuery : simpleCarrousel.js")
