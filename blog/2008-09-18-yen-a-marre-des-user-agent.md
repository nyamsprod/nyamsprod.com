---
title: "Y'en a marre des User Agent"
date: "2008-09-18"
categories: 
  - "web"
tags: 
  - "browser"
  - "javascript"
  - "navigateur"
  - "user-agent"
  - "yen-a-marre"
---

Je ne vais pas refaire pour vous l'historique des User Agent, [d'autres l'on fait bien mieux que moi](http://www.webaim.org/blog/user-agent-string-history/ "L'histoire complète des user agent"). En résumé cette chaine de caractères qui se retrouve dans tous nos navigateurs ne sert plus à rien. C'est un bordel immonde dont il faudrait s'affranchir une bonne fois pour toute. [![](images/complique-203x300.jpg "pourquoi faire simple quand on peut faire compliqué")](http://www.nyamsprod.com/blog/wp-content/uploads/2008/09/complique.jpg)Pourquoi je vous en parle aujourd'hui alors ? C'est simple, comme vous le savez probablement tous maintenant, Google a sorti son propre navigateur, Chrome, pour ne pas le citer. Bien que ce navigateur [soit en béta](http://nyams.planbweb.com/blog/2008/04/22/yen-a-marre-des-beta/ "y'en a marre des logiciel en béta"), le buzz autour de celui-ci ne fini pas d'être entretenu par l'une ou l'autre prédiction sur sa suprématie avenir. Cela me rappelle les même estimations et la même agitation que l'on a connu à l'époque de [la sortie de Google Talk](http://googlesystem.blogspot.com/2006/08/why-google-talk-will-be-best-instant.html "Pourquoi Google Talk sera le meilleur") et l'on sait depuis ce qu'il en est advenu de la suprématie de Google Talk. Mais là, je m'égare. On est en 2008 et cela va faire plus de 8 ans que l'on préconise [l'arrêt de la détection des navigateurs via leur user agent](http://www.quirksmode.org/js/support.html "Pourquoi c'est mal de détecter un navigateur via son user agent") mais cela [n'empêche pas certains](http://www.bostral.com/1319-comment-trouver-chrome-avec-une-fonction-javascript.html "Comment trouver Chrome avec une fonction Javascript") de continuer à utiliser cette méthode pour Chrome. La détection des capacités réelles du navigateur ou **Object Detection** est la seule et unique manière d'obtenir un script javascript simple et facile à maintenir. A bon entendeur salut.
