---
layout: post
title: "jsplayer sur github"
date: "2009-03-09"
categories: 
  - "web"
tags: 
  - "audio"
  - "github"
  - "html5"
  - "jsplayer"
  - "mediacontroller"
  - "video"
---

Je viens de mettre sur github mon premier code Javascript. J'espère que ce n'est que le premier d'une longue série, le futur nous le dira :) . Pour une première fois j'ai décidé de partager mon script en version améliorer d'utilisation des balises média du html5. Une fois n'est pas coutume, je reviens sur un article que j'avais publié il y a quelques temps sur ce site à propos de l'[utilisation de la balise video](http://nyamsprod.com/blog/2009/01/05/utilisation-de-la-balise-video/ "Utilisation de la balise video") du html5. A l'époque il m'avait fallu 3 heures de code pour mettre en place un script permettant de contrôler l'insertion et l'utilisation d'un média au format ogg sous Firefox 3.1 beta 2 . Ce code bien que fonctionnel présentait beaucoup de lacunes.

- Il ne fonctionnait que sous Firefox 3.1 beta 2, alors que les balises _media_ sont reconnus et utilisables depuis bien longtemps sous Safari;
- Il fonctionnait un peu comme [swfobject](http://code.google.com/p/swfobject/ "Documentation sur la dernière version de swfobject") alors que les balises _media_ ne s'utilisent pas comme la balise `object` lorsqu'elle inclue un composé Flash dans une page HTML;

J'ai d'abord amélioré le code in-situe et celui-ci à rapidement augmenté en taille et en fonctionnalité De fait,  le code présenté par l'article n'a plus rien à voir avec le code présent sur la page d'exemple :) . Depuis j'ai encore amélioré le code pour combler les lacunes mentionnées plus haut et en résumé, la fonction a changé de nom, et son utilisation a drastiquement évolué.

Pour lire, télécharger, tester, cloner, modifier et améliorer _jsplayer_ il n'y a qu'une seule adresse à suivre sur [GitHub](http://github.com/nyamsprod/jsplayer/tree/master "Le code source de jsplayer sur GitHub"). je vous donne néanmoins un lien avec l'[exemple que j'ai posté sur GitHub](http://nyamsprod.com/test/jsplayer/ "Page de test de jsplayer") au cas où vous vous demandez ce que cela donne.

Je rappelle au passage pour bien comprendre l'exemple que ce script ne fonctionne que sous un navigateur qui reconnait :

- les balises media ( à l'heure où j'écris ces quelques lignes il s'agit de Firefox 3.1 beta 2 et les versions supérieurs, Safari 3.1 et les versions supérieurs);
- les méthodes javascript querySelector (ce qui élimine toutes les versions d'Opera sauf Opera 10) et addEventListener (ce qui élimine toutes les versions de Internet Explorer);

Si votre navigateur pour l"une ou l'autre raison ne reconnait pas l'une ou l'autre méthode et/ou balise mentionnée ci-dessus et que vous avez, comme j'ai fais dans mon exemple, une balise `object` ou `embed` à l'intérieur de votre balise média, c'est cette balise qui sera utilisée en lieu et place de mon script. Rien ne vous empêche, au contraire, d'étendre les fonctionnalités de _jsplayer_ à d'autres navigateurs, si ceux-ci supportent au moins les balises media du html5.
