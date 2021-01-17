---
layout: post
title: "PNG, IE, et mon site ne font pas bon ménage - mise à jour"
date: "2007-12-09"
categories: 
  - "web"
tags: 
  - "bug"
  - "internet-explorer"
  - "png"
---

Ceci est un petit article, juste pour dire que j'ai enfin compris le bug d'affichage sous IE de mon ancien logo en png. Pour ce qui ne s'en rappellent pas, allez jeter un coup d'oeil sur [mon ancien poste](http://nyamsprod.com/blog/2007/01/15/png-ie-et-mon-site-ne-font-pas-bon-menage/ "PNG, IE, et mon site ne font pas bon ménage - partI") ;) . En résumé, Trident possèdent à la base 2 problèmes avec le format png, le premier problème, résolu avec IE7, est celui de la couche alpha des images au format png de 24-bits. Le second, qui n'est toujours pas résolu est à l'origine de mon bug d'affichage, [c'est le bug gAMA](http://hsivonen.iki.fi/png-gamma/ "The Sad Story of PNG Gamma “Correction”") . Ce bug serait également visible sous d'anciennes versions de Safari ( avant Webkit) , de Gecko et d'Opera, ce que je ne savais pas à l'époque :

- puisque je n'ai pas de Mac;
- puisque je n'utilise que les versions les plus récentes de ces différents navigateurs.

De plus, les autres moteurs de rendus ont soit étaient mise à jour, soit étaient changés pour, entre autre, résoudre ce bug. Donc comme je l'avais deviné à l'époque, c'était bien un problème de moteur de rendu ( encore un vous me dirait...). Comme je n'ai pas le temps et encore moins l'expertise pour traduire fidèlement [la raison technique de ce problème](http://www.easy-reader.net/archives/2006/02/18/png-color-oddities-in-ie/ "Une autre illustration du gAMA bug") je vous invite à découvrir une autre manière de [résoudre le gAMA bug](http://blog.reindel.com/2006/12/29/remove-the-gamma-gama-chunk-from-a-png-image-to-fix-darker-colors-in-ie/ "Résolution du problème en modifiant le png") pour contenter IE6 et IE7, les derniers navigateurs à encore afficher le bug, en attendant la nouvelle monture de _IE8_ ou _IE.Next_ qui, [d'après les déclarations de la IE Team](http://www.broken-links.com/2007/10/03/ienext-to-get-a-new-layout-engine/ "l'annonce du nouveau moteur de rendu pour IE8"), ne devrait plus contenir ce bug vu qu'il vont changer de moteur de rendu.

PS : IE Team ne me fait pas regretter l'espoir que je mets en vous ;)
