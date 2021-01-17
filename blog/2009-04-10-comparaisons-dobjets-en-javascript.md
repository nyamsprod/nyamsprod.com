---
title: "Comparaisons d'objets en javascript"
date: "2009-04-10"
categories: 
  - "web"
tags: 
  - "argumentscallee"
  - "comparaison"
  - "hasownproperty"
  - "instanceof"
  - "javascript"
  - "objet"
  - "operator"
  - "tostring"
  - "typeof"
---

Une des questions que j'aime à poser aux  jeunes développeurs qui viennent passer une interview d'embauche chez nous est _quelle est la différence entre l'opérateur (`==`) et l'opérateur (`===`)_ ?. En _javascript_ comme en _PHP_, la réponse et la même le premier pratique une conversion silencieuse des valeurs que l'on compare tandis que l'autre ne le fait pas. Dans un monde idéal **on devrait donc toujours utiliser l'opérateur `===` pour comparer 2 valeurs**. Mais seulement voila essayer de comparer 2 objets en _javascript_ en utilisant cet opérateur et [vous aurez une petite surprise](https://developer.mozilla.org/fr/R%C3%A9f%C3%A9rence_de_JavaScript_1.5_Core/Op%C3%A9rateurs/Op%C3%A9rateurs_de_comparaison "Opérateurs de comparaison"). C'est simple, à moins que les 2 objets fassent référence au même objet l'opérateur retournera systématiquement `false`. En d'autre terme, si comme moi vous désirez **savoir si 2 objets distinctes sont similaires** l'opérateur `===` ne fonctionne pas, tout comme l'opérateur `==` d'ailleurs. Vu qu'aucune solution _out of the box_ existe en `javascript`, je me suis résolu à créer une fonction qui me permettrait de répondre à ma question le plus facilement possible.

**Pour que 2 objets soient similaires il faut que les méthodes et les propriétés qu'ils contiennent soient identiques.** Donc suivant tout bêtement mon raisonnement je suis arrivait à la fonction suivante:

\[code language='javascript'\]function isObjectsEquals(a, b) { var isOK = true; for (var prop in a) { if (a\[prop\] !== b\[prop\]) { isOK = false; break; } } return isOK; };\[/code\]

Ce code fonctionne mais il est trop incomplet. Disons-le clairement, je suis à la recherche d'un code assez robuste pour pouvoir l'inclure dans ma librairie de fonctions que j'utilise dans mes projets _javascript_, je recherche donc une fonction **bullet proof**. D'où, les optimisations que je lui est apportées. Ma première optimisation a été de vérifier _uniquement_ les méthodes réellement spécifique à l'objet et non les méthodes héritées du fait que l'on utilise un objet. Je suis passé à la fonction intermédiaire suivante :

\[code language='javascript'\]function isObjectsEquals(a, b) { var isOK = true; for (var prop in a) { if (a.hasOwnProperty(prop)) { if (a\[prop\] !== b\[prop\]) { isOK = false; break; } } } return isOK; };\[/code\] _[On devrait toujours utiliser](http://javascript.crockford.com/code.html "Conventions de bon codage en Javascript") `hasOwnProperty` lorsque l'on boucle en javascript sur un objet, pour ceux qui ne le savent pas ;) ._

L'optimisation suivante est en rapport avec la comparaison effectuée à l'intérieur même de ma fonction. Les plus perspicaces d'entre vous auront noté que j'utilise _encore_ un opérateur de comparaison. Et donc je n'ai fait que déplacé le problème initial. Que se passerait-il si l'une des méthode de mon objet était un objet en soit ? Tout ce travail n'aurez donc servi à rien. Pour remédier à cela il faudrait déterminer le type des méthodes de l'objet et au cas échéant procéder à un appel récursif à ma fonction. Sans aller dans les détails, il se trouve que l'utilisation des fonctions [`typeof` et `instanceof` est déconseillée](http://thinkweb2.com/projects/prototype/instanceof-considered-harmful-or-how-to-write-a-robust-isarray/ "`instanceof` considered harmful (or how to write a robust `isArray`)"), il faut plutôt se fier à `Object.prototype.toString`, une propriété interne de tout objet en `javascript`, pour déterminer à coup sûr le type d'une variable. De fait ma fonction finale ressemble à ceci :

\[code language='javascript'\]function isObjectsEquals(a, b) { var prop, otype, isOK = true; for (prop in a) { if (a.hasOwnProperty(prop)) { otype = Object.prototype.toString.call(a\[prop\]).match(/^\[objects(.\*)\]$/)\[1\]; isOK  = (!/^(String|Number|Window)$/.test(otype)) ? arguments.callee(a\[prop\], b\[prop\]) : (a\[prop\] === b\[prop\]); if (isOK !== true) { break; } } } return isOK; };\[/code\]

Et voila. Et comme cette fonction est toute jeune, si il y a parmi vous des volontaires pour la tester et pourquoi pas trouver des bugs pour l'améliorer, je serais le premier ravi car pour l'instant elle fonctionne dans tous mes tests ;)
