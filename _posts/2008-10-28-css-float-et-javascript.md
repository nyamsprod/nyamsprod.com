---
layout: post
title: "Assigner ou récupérer la valeur de l'attribut CSS float via Javascript"
date: "2008-10-28"
categories: 
  - "web"
tags: 
  - "attribut"
  - "browser-detection"
  - "css"
  - "cssfloat"
  - "float"
  - "javascript"
  - "object-detection"
  - "stylefloat"
---

Comment manipuler la propriété CSS `float` via _javascript_. La réponse qui vient directement à l'esprit est de dire qu'il suffit d'écrire :

\[sourcecode language='javascript'\]var el = document.getElementById('element\_id'); el.style.float = 'left';\[/sourcecode\]

Si cela était aussi simple, ce poste ne servirait à rien ;) . En effet le code ci-dessus ne fonctionne pas pour la simple et bonne raison qu'en _javascript_ comme dans la plupart des langages de programmation le mot `float` est un mot réservé. En effet, `float` désigne un nombre décimal. Alors comment faire ?

Un peu d'histoire pour commencer. L'élaboration de la classe _style_ en DOM pour récupérer et assigner les valeurs des feuilles de style est un apport de _Microsoft_. Et lorsque les développeurs de _M$_ ce sont retrouvés confrontés à ce problème, ils l'ont résolu en créant la méthode spécifique `styleFloat`. Ainsi, historiquement pour assigner et/ou récupérer la propriété `float` d'un élément il fallait écrire, dans le premier navigateur à permettre une telle assignation, le code suivant :

\[sourcecode language='javascript'\]var el = document.getElementById('element\_id'); el.style.styleFloat = 'left';\[/sourcecode\]

Mais voila, entre temps, le W3C a récupéré et a reformulé la classe `style` et, après moultes débats, il fut décidé d'utiliser la méthode `cssFloat`. Donc selon le W3C il faut écrire ce qui suit :

\[sourcecode language='javascript'\]var el = document.getElementById('element\_id'); el.style.cssFloat = 'left';\[/sourcecode\]

Bon je vois déjà, certains d'entre vous critiquer encore une fois Microsoft, mais pour une fois, je vais prendre leur défense. Ils ont créé et implanté la classe `style` avant les recommandations du W3C et donc ils ont fait ce qu'ils ont jugé être correct à l'époque, et d'ailleurs d'autres navigateurs ont suivi et ont implanté la méthode `styleFloat` .

En résumé, à l'heure actuelle, il existe 3 types de navigateurs:

- Ce qui ne connaissent que la méthode `styleFloat`, comme Internet Explorer jusqu'à la version 7 (_je n'ai pas testé Internet Explorer 8_). 
- Ce qui ne reconnaissent que la méthode `cssFloat` , comme Safari ou encore Firefox,
-  Et enfin, ceux qui comprennent les 2 méthodes, Opera est dans cette dernière catégorie. [](http://nyamsprod.com/test/float/ "Démonstration de l'assignation et de la récupération de la valeur float")

[Dans de telles conditions](http://nyamsprod.com/test/float/ "Démonstration de l'assignation et de la récupération de la valeur float"), on serait tenté d'utiliser les _user agent_ des navigateurs pour déterminer quand utiliser l'une ou l'autre de ces méthodes, [mais cet option est mal](http://nyamsprod.com/blog/2008/09/18/yen-a-marre-des-user-agent/ "Il est temps d'arrêter d'utiliser les user agent")!! Au lieu de cela, le plus simple et le plus efficace est encore d'écrire les codes suivants :

\[sourcecode language='javascript'\]var el = document.getElementById('element\_id'); //assignation

el.style.styleFloat = 'left';

el.style.cssFloat = 'left'; //récupération

var elFloat = (typeof el.style.cssFloat === 'string') ? el.style.cssFloat : el.style.styleFloat;\[/sourcecode\]

En résumé, lors de l'assignation, on utilise les 2 méthodes, même si cela ajoute la méthode manquante à l'élément sélectionné, cela n'engendrera aucune erreur DOM et/ou javascript. Lors de la récupération de la valeur de _float_ il suffira de vérifier si la méthode `cssFloat` est présente si oui on récupère sa valeur, sinon on récupère la valeur de `styleFloat`.
