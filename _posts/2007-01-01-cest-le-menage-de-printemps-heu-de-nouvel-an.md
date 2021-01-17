---
layout: post
title: "C'est le ménage de printemps... heu de Nouvel An"
date: "2007-01-01"
categories: 
  - "humeurs"
tags: 
  - "blog"
  - "cocmes"
  - "rss"
---

#### Mon RSS aggregator perso

Vue que c'est généralement en fin d'année qu'on fait le tri de ce qui va ou pas. C'est ce que j'ai fait sur mon site. Donc j'en profite pour mettre en lumière des projets que je n'ai pas terminé par manque de temps. Si il y a des personnes pour les terminer merci de me le dire, je pourrais fournir les codes si certains sont cachés.

[Mon RSS aggregator](/aggregator/)

L'idée de cette application m'est venu en découvrant les fonctions XML de Firefox et en m'apercevant que Internet Explorer possédaient des fonction similaires ( ou le contraire ) cela dépend de la manière dont on considére ces 2 navigateurs.Bref la majorité du script est réalisé via DOM par le navigateur. avec le serveur servant de proxy pour récuperer les flux. Bien sur un système de cache est utilisé pour ne pas trop faire ramer le serveur ;).Cette application ne fonctionne que sous Firefox et sous Internet Explorer 6 et 7. Sur Opera ça fonctionne pas... donc il faudrait voir ce qu'y peut être fait pour y remédier. Comme je ne possède pas de Mac. Je ne connais pas le comportement de ce script sour Safari. Mais je pense pas que cela fonctionne.

#### A propos de cocmes reloaded

J'ai terminé la mise à jour de mon site interne du [cocmes](/cocmes/) en rajoutant toutes les rubriques qui manquaient et en m'amusant en rajoutant des stats et des liens partout vraiment pour faire style le site est trop complet. Le site comporte maintenant :

- Un flux RSS
- Les résultats, le classement et les statistiques principales pour toutes les divisions du cocmes;
- Les résultats, le classement et les statistiques principales pour tous les tournois;
- Une présentation de toutes les équipes et de leur calendrier de rencontres;
- Les statistiques générales sur l'ensemble de la saison et un graphe de résumé;

Le site se comporte à l'identique sur toute les plateformes _et_ utilise très peu de ressources gràce à un système de cache et aux outils suivants :

- [mysql](http://www.mysql.com "le site officiel de MySQL") ,
- [smarty](http://smarty.php.net/manual/fr/ "le site officiel de Smarty"),
- [jpgrah](http://www.aditus.nu/jpgraph/ "le site officiel de Jpgrah"),

Et grâce à une bonne utilisation du [XHTML](http://nyamsprod.com/xhtml.html) , du [DOM](http://nyamsprod.com/dom.html) et du CSS

#### De manière générale

Après cette promo tout azimut, je tiens également à signaler à ceux qui l'ont pas encore remarquer que j'ai mis légèrement à jour les feuilles de style du site : **J'ai décidé de ne plus tenir compte de Internet Explorer 6** vue que IE7 est sortie et que c'est vraiment un pas de géant de la part de Microsoft vers la bonne direction. J'ai également enlevé du contenu que je n'utilise plus ou qui n'avait plus d'intérêt à se trouver sur le site.
