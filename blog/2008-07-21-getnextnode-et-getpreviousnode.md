---
title: "getNextNode, getPreviousNode ou comment compléter les méthodes relationnelles du DOM"
date: "2008-07-21"
categories: 
  - "web"
tags: 
  - "astuce-javascript"
  - "dom"
  - "dom1"
  - "javascript"
  - "librairie"
  - "librairie-javascript"
  - "nextsibling"
  - "previoussibling"
---

Je vous présente 4 fonctions javascript que vous pourriez ajouter à votre librairie javascript personnelle. Elles ont pour but de compléter les méthodes relationnelles d'un élément sélectionnés via DOM.

En tant que programmeur javascript on est régulièrement amené à déterminer l'élément qui suit ou qui précède l'élément que l'on a sélectionné. Pour se faire le [DOM Core Level I](http://nyams.planbweb.com/tutorial/dom/ "Didactitiel simplifié sur le DOM") nous permet de déterminer ces éléments en utilisant 2 méthodes [`previousSibling` et `nextSibling`](http://nyams.planbweb.com/tutorial-dom-07.html#siblings "explication du fonctionnement du previousSibling et  de nextSibling"). Le seul problème avec ces 2 méthodes est qu'en DOM les espaces sont considérés comme étant des élément à part entière. Du coup l'utilisation de ces 2 méthodes est rendu quasi inutile car ce que l'on recherche la plupart du temps c'est le prochain élément et non les espaces blancs qui l'entoure ;) .Pour contourner se problème j'ai écrit 2 fonctions que j'utilise de manière fréquentes et qui réponde à ce problème. La fonction `getNextNode` qui détermine l'élément, le tag qui suit : \[sourcecode language='javascript'\]function getNextNode(el) { var node = null; if (el.nextSibling) { node = el; do { node = node.nextSibling; } while (node.nodeType !== 1 && node.nextSibling); } return (node.nodeType === 1) ? node : null; };\[/sourcecode\]

Et la fonction `getPreviousNode` qui détermine l'élèment qui précède l'élément/tag détecté.

\[sourcecode language='javascript'\]function getPreviousNode(el) { var node = null; if( el.previousSibling) { node = el; do { node = node.previousSibling; } while (node.nodeType !== 1 && node.previousSibling); } return (node.nodeType === 1) ? node : null; };\[/sourcecode\]

Notez, que si aucun élément n'est trouvé, ces 2 fonctions retournent `null`. Et voilà avec ces 2 petites fonctions il vous sera très facile de connaître l'élèment suivant ou précédent votre tag. De plus en y réfléchissant bien et sur base de ces 2 fonctions on peut facilement ajouter 2 autres fonctions tous aussi utiles `getFirstNode` pour déterminer la première balise d'un élément :

\[sourcecode language='javascript'\]function getFirstNode(el) { var node = null; if (el.hasChildNodes()) { node = el.firstChild; if (node.nodeType !== 1) { node = getNextNode(node); } } return node; }\[/sourcecode\]

et  `getLastNode` pour déterminer le dernier élément d'une balise et voila :

\[sourcecode language='javascript'\]function getLastNode(el) { var node = null; if (el.hasChildNodes()) { node = el.lastChild; if (node.nodeType !== 1) { node = getPreviousNode(node); } } return node; }\[/sourcecode\]
