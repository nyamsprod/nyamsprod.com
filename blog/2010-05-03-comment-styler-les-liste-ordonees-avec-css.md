---
title: "Comment styler les listes ordonées en CSS"
date: "2010-05-03"
categories: 
  - "web"
tags: 
  - "counter-increment"
  - "counter-reset"
  - "css2-1"
  - "css3"
  - "liste-ordonnees"
  - "navigateurs"
---

Une question qui revient régulièrement et qui est la hantise de tout bon Webdesigner est comment faire pour rendre agréable une liste ordonnée en CSS. La différence entre une liste ordonnée et une liste non-ordonnée est dans le mot ordonnée :) _(bravo pour cette Lapalissade nyamsprod)_. Cela parait trivial à dire mais cela a des conséquences importantes ainsi il est de coutume pour maitriser au mieux une liste de "remettre à zéro" ses propriétés de style. Cela se fait très simplement en utilisant le code qui suit:

\[sourcecode language="javascript"\]ol, ul { margin:0; padding:0; list-style:none; }\[/sourcecode\]

Mais une fois appliquée, cette règle a pour conséquence de faire disparaitre la notion de liste ordonnée car les repères de numérotation ont disparu. Jusqu'à très récemment le _"hack"_ pourrave utilisé pour contourner cette difficulté était simplement de renommer au niveau de chaque élément de liste son ordre, cela avait pour effet d'enlever l'utilité sémantique de la balise `ol`. Mais tout cela c'est du passé, vu que **tous les navigateurs modernes supportent le CSS 2.1** il existe maintenant une méthode simple et efficace pour récupérer les fonctionnalités perdues voire en ajouter d'autres encore plus intéressantes. Laissez-moi vous présenter les propriété `counter-*` du CSS 2.1.

Comme un exemple vaut mieux qu'un long discours, je vous présente [la recette pour faire une omelette](http://nyams.planbweb.com/test/css/list-css.html "exemple d'utilisation des propriétés counter-* de CSS 2.1") que je viens de copier/coller sur un site de recette. En utilisant les propriétés du CSS 2.1 content et la pseudo class `:before` en conjonction avec les propriété `counter-*`, je retrouve facilement la numérotation des étapes et en bonus je peux rajouter des effets de style qui m'étais impossible avec la propriété `list-style` .

\[sourcecode language="javascript"\]ol { margin:0; padding:5px; list-style:none; counter-reset:section; } li:before { content: counter(section) " "; counter-increment:section; }\[/sourcecode\]

la variable `section` peut prendre n'importe quel nom et sert uniquement à garder et a incrémenter la variable utilisée pour afficher la numérotation via la propriété `content` et la fonction `counter`.

Et, pour les chanceux avec un navigateur qui supporte certaines propriétés du CSS3 on  pourra encore mieux visualiser la recette en survolant les instructions, bonne appétit ;) .

[Voir l'exemple final](http://nyams.planbweb.com/test/css/list-css.html "exemple d'utilisation des propriétés counter-* de CSS 2.1")

_PS: n'hésitez pas à triturer le code source pour comprendre comment j'ai fait._
