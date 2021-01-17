---
title: "Transparence et opacité dans les navigateurs récents"
date: "2007-11-22"
categories: 
  - "web"
tags: 
  - "css-3"
  - "navigateurs"
  - "opacite"
  - "transparence"
---

Je viens de mettre à jour le design de mon site, et j'en ai profité pour le rendre homogène. La seule différence étant que pour la partie blog, j'ai ajouté une image en arrière plan. Et comme j'aime me faire plaisir j'ai voulu la faire ressortir via transparence à travers les textes et contenus média de mon blog. Voici en quelques sortes le résultat de mes investigations en utilisant les **Big4**.

Tout d'abord, pour être clair j'appelle les _Big4_ les 4 moteurs de rendus des navigateurs les plus répandus dans le monde PC sous windows, c'est-à-dire _Trident_ pour Internet Explorer 6 et 7 , _Gecko_ pour Mozilla firefox, _Presto_ pour Opera et _Webkit/KHTML_ pour Safari. Je vais parler de la propriété CSS : **opacity,** celle-ci fait partie de la spécification de CSS3 et donc n'est pas standard au CSS2 ou au CSS2.1 mais les _Big4_ prétendent avoir déjà intégré avec succès cette propriété. Cet article va donc nous indiquer si les prestations sont à la mesure des prétentions affichées par les _Big4_ :) . Enfin pour en terminer avec mon introduction voici comment, selon le W3C, on doit définir la propriété de transparence via l'attribut _opacity_.

Pour un élément **p** par exemple on écrira :

`p { opacity:0.9; } avec une valeur comprise entre 0 et 1.`

Lorsque _opacity équivaut à 1_ l'opacité est **maximale**, il n'y a pas de transparence, _c'est le comportement par défaut_. Lorsque _opacity équivaut à 0_ l'opacité est **minimale**, la transparence est maximale, la balise est son contenu ne sont plus visibles.

Afin de tester les _Big4_, [j'ai créé une page qui me servira de test](http://nyams.planbweb.com/test/opacity/ "la page de test de l'opacité"), et ma conclusion est sans équivoque, Gecko est le seul des _Big4_ a passer mon simple test haut la main, mais voyons cela en détail.

[![](images/ie.thumbnail.png)](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/trident.jpg "le rendu de la page sous Trident") **\- [Trident/Internet Explorer 6 et 7](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/trident.jpg "le rendu de la page sous Trident"):** le problème avec Trident c'est qu'il permet l'utilisation de l'opacité que via l'utilisation de directX donc en fait on écrit par réellement du CSS , d'ailleurs le vérificateur syntaxique du W3C vous le rappellera dès que vous essayerez de valider votre feuille de style.

Pour le même élément **p** sous Trident il faudra écrire ceci :

`p { filter:alpha(opacity=90); }`

L'opacité varie entre des entiers compris entre 0 est 100 avec une opacité maximale pour la valeur 100 et une transparence maximale pour la valeur 0.

Franchement, ils auraient pu faire mieux. d'autant que sous Internet Explorer 7, parmi les tonnes de bug fixes effectués par la IE Team, celui-ci n'a pas été corrigé. A croire que Trident ne pouvait pas être amélioré dans ce cas précis. Donc _filter_ subsiste mais avec un twist. Depuis Vista, Windows a, enfin, introduit le lissage des polices de caractères ou ClearType, par défaut sur sa plateforme, fonction qui existait déjà pour Mac OS X, par exemple. Hé bien comble de malheur pour nous, si vous utilisez l'opacité, vous perdez le ClearType pour la page. Donc les avancées de Windows sont contrecarrés par l'opacité, dingue non!!!

**Les autres navigateurs supportent l'utilisation CSS de l'attribut opacité tel que recommandé par le W3C.**

[![](images/presto.thumbnail.png)](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/presto.jpg "le rendu de la page sous Presto") **\- [Presto/Opera](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/presto.jpg "le rendu de la page sous Presto")** : J'aurais pu mettre ce navigateur au début de ma liste, car j'estime que c'est le plus mauvais de tous dans mon test du moins. Pourquoi, parce que Opera s'emmèle les pinceaux dès qu'il s'agit d'opacité. D'une part sous Vista il réagit comme IE 7, il perd le lissage des polices de caractère. D'autres part, lorsque vous avez l'outrecuidance d'ajouter un contenu multimédia, via la balise object ( une animation Flash ou Silverlight, ou que sais-je...) l'opacité s'emballe et vous avez beau mettre un faible niveau d'opacité, votre composé multimédia sera quasiment illisible. Bref l'opacité vous empêche toute inclusion d'objets multimédias dans votre page.

[![](images/webkit.thumbnail.png)](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/webkit.jpg "le rendu de la page sous Webkit/Safari 3.0 beta pour Windows") **\- [Webkit/KHTML/Safari](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/webkit.jpg "le rendu de la page sous Webkit/Safari 3.0 beta pour Windows") :** Le comportement de Safari sous Windows, m'interpelle moins, même si celui-ci est plus radical qu'Opera. la transparence est correcte, Webkit garde le ClearType mais il refuse tout simplement d'afficher votre contenu multimédia. Donc tout comme Opera , il empêche l'inclusion d'objet multilmédia dans votre page. Mais, au moins à la différence d'Opera, il ne vous met pas, totalement dans l'embarras, quoiqu'il garde l'espace de votre contenu vide. Bref un comportement plus sain, à mon avis, mais tout aussi bizarre. Notez, que si vous faites un clique droit dans l'espace où l'objet multimédia aurait du se trouver, Webkit vous le rappelle en indiquant bien qu'il est en train d'afficher du Flash ( c'est le cas de mon exemple ), vraiment le comportement de ce moteur d'affichage est bizarre.

[![firefox.png](images/firefox.thumbnail.png)](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/gecko.jpg "le rendu de la page sous Gecko")\- **[Gecko/Mozilla Firefox](http://www.nyamsprod.com/blog/wp-content/uploads/2007/11/gecko.jpg "le rendu de la page sous Gecko") :** la transparence est nickel, le lissage des caractères perdure, le contenu multimédia est toujours présent et accessible , bref c'est le gagnant du jour.

Encore une fois, cela est le comportement sous Windows Vista/XP/2000 , je n'ai pas étudié ce comportement sous MacOS X, je n'ai pas de Mac sous la main, ou sous GNU Linux et autre Unix-Like, pourtant je travaille avec Ubuntu. Donc si vous avez la possibilité de tester ma page et de me donner un compte rendu, je le rajouterai ici sans problème.

Bref, finalement j'ai eu recours à un _hack_, dont je ne suis pas fier pour quand même avoir ma transparence sous Gecko uniquement, vue les lacunes des autres navigateurs. Je suppose que cela ne fonctionnera pas toujours dans les versions futures de Gecko, donc **ne l'utilisait pas**, du moins je ne le recommande à personne, avant d'avoir bien compris les implications de son utilisation. Il "suffit" de préfixer la propriété `opacity` avec `-moz-` pour faire un "_rollback_" sur la propriété `-moz-opacity` spécifique à Gecko. Il faut comprendre que dès que cette attribut sera retiré des versions ultérieures de Gecko, se hack ne fonctionnera plus . Ce hack est loin d'être la solution idéale, mais bon, je dois dire que je ne suis pas fan des hacks à la base donc je suis très mauvais pour en créer des bons.
