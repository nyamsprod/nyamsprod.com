---
layout: post
title: "Internet Explorer 8 débarque enfin"
date: "2009-01-28"
categories: 
  - "web"
tags: 
  - "addeventlistener"
  - "attachevent"
  - "css"
  - "developpeurs"
  - "firefox"
  - "html"
  - "ie6"
  - "ie7"
  - "ie8"
  - "internet-explorer"
  - "javascript"
  - "navigateurs"
  - "opera"
  - "safari"
  - "yen-a-marre"
---

Maintenant que [IE8 est passer en mode RC1](http://blogs.msdn.com/ie/archive/2009/01/26/internet-explorer-8-release-candidate-now-available.aspx "L'annonce officielle de la sortie de la RC1 de Internet Explorer 9"), à moins d'un terrible bug de régression plus aucune nouveauté n'est attendue avant la sortie de la version définitive du successeur de IE7. Je profite donc de ce moment d'apparente accalmie pour revenir sur certains aspects d'IE8, du point de vue d'un développeur.

[![La nouvelle fenêtre de dialogue d'erreur d'IE8](images/ie8error-300x198.jpg "La nouvelle fenêtre de dialogue d'erreur d'IE8")](http://www.nyamsprod.com/blog/wp-content/uploads/2009/01/ie8error.jpg)Tout d'abord, IE8 est le premier navigateur de Microsoft qui vient équiper de l'onglet spécifique pour développeurs désormais indispensable pour tout navigateur moderne qui se respecte. Cet onglet possède comme sur les autres navigateurs des outils pour débusquer les problèmes de  votre page  sous IE. C'est la fin des alertes incompréhensibles sous IE. IE8 nous informe comme les autres navigateurs de l'origine exacte de l'erreur. Et rien que cette avancée sera, sans nul doute, saluée par tous les développeurs.

Une autre nouveauté de IE8 est son respect de [la norme CSS 2.1](http://www.w3.org/TR/CSS21/ "Les recommandations du W3C pour le CSS 2.1"), tel que spécifiée par le _W3C_. La IE Team va jusqu'à indiquer que [IE8 est le navigateur le plus stricte par rapport au recommandation du W3C au niveau du CSS 2.1](http://blogs.msdn.com/ie/archive/2009/01/27/microsoft-submits-thousands-more-css-2-1-tests-to-the-w3c.aspx "Internet Explorer 8 serait le navigateur le plus respectueux de la norme CSS 2.1"). En clair, vous pouvez sans crainte utiliser votre CSS pour Firefox ou Opera directement dans IE8 et les rendus seront alors identiques... à l'exception de toutes les déclarations en CSS3 qui ne seront pas comprises par IE8.. au grand malheur de certains :) . Pour ma part, je préfère regarder le verre à moitié plein et je me dit que dorénavant, le CSS 2.1 représente le fondement de tout code CSS pour la création d'une feuille de style. Il ne sera donc plus acceptable de ne pas savoir et/ou utiliser les pseudo-class comme `:before` et `:after` par exemple. C'est peut-être une révolution muette, qui passera sans doute inaperçue, dans le grand public, mais elle est de taille du point de vue des développeurs.

IE8 passe l'[Acid Test 2](http://www.webstandards.org/action/acid2/ "L'Acid Test 2 expliqué"). Bien que j'ai certaines réserves qu'en à ce type de test, le fait que IE8 soit capable de le passer nous permet d'enfin pouvoir utiliser la balise `object`, [dans toutes sa plénitude](http://nyamsprod.com/blog/2009/01/23/inserer-une-image-en-utilisant-la-balise-object/ "Utiliser la balise obejct pour insérer une image"), et d'autres techniques bien utiles qui nous étaient jusqu'alors impossible d'implanter du fait des moteurs de rendu lamentables qui équipent les anciennes versions de IE. _Pour mémoire, la série des Firefox 2 n'a jamais passé l'Acid Test 2 et pourtant Firefox 2 est considéré comme meilleur que IE7 voire IE8_ ;) .

Le vrai problème avec IE8 c'est le _javascript_. IE8 présente beaucoup de nouveautés, [j'en ai même présenté certaines sur mon site](http://nyamsprod.com/blog/2009/01/21/parcourir-un-document-html-en-utilisant-dom/ "Comment utiliser querySelector et querySelectorAll"), mais **La grosse faiblesse de IE8** réside ailleurs. [En 2000 le W3C publié le modèle de gestion évènement en javascript](http://www.w3.org/TR/DOM-Level-2-Events/ "Les recommandations du W3C pour la gestion des évènements"), en introduisant des fonctions comme `addEventListener`, **9 ans plus tard**, [IE8 n'implante toujours pas ces méthodes](http://connect.microsoft.com/IE/feedback/ViewFeedback.aspx?FeedbackID=333958 "Le bug le plus important qui ne sera pas résoud sous IE8") bien que tous les autres navigateurs les utilisent. Cela pose un problème majeur, que chaque framework javascript essaie de résoudre tant bien que mal. Mais la seule et unique manière de résoudre ce problème c'est que la IETeam implante cela dans son navigateur. Certains développeurs exaspérés par l'attitude d'éditeur de Redmond ont réclamés, en vain, [l'inclusion de ces méthodes avant toute sortie de IE8](http://www.robertnyman.com/2008/11/04/internet-explorer-8-fix-event-handling-or-dont-release-it/ "IE 8 : réglé le problème de la gestion des évènement ou ne sorter pas ce navigateur!!"), mais visiblement la IE Team ne les a pas écoutés.

IE7 était en son temps censé contenté les intégrateurs avec un respect accru des règles de CSS. Finalement il aura fallu attendre IE8 pour que les intégrateurs soit plus ou moins satisfait du résultat. IE8 était censé contenter les développeurs de script javascript, il nous faudra donc attendre IE9 pour cela. Mais en attendant, ne boudons pas notre plaisir, avec la fin de l'utilisation des expressions  en CSS, avec l'abandon d'attribut propriétaire comme `allowtransparency` et à l'utilisation enfin possible de l'attribut `disabled` sur la balise `option` bien sur toute cela en mode standard de IE8.
