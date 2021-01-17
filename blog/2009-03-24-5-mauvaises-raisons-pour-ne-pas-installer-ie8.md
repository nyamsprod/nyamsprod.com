---
title: "5 mauvaises raisons pour ne pas installer IE8"
date: "2009-03-24"
categories: 
  - "web"
tags: 
  - "acid-test"
  - "addevent"
  - "addeventlistener"
  - "beta"
  - "border-radius"
  - "chrome"
  - "css"
  - "firefox"
  - "internet-explorer-8"
  - "javascript"
  - "opera"
  - "safari"
  - "yen-a-marre"
---

Maintenant que Internet Explorer 8 est téléchargeable, ça y est, tout le monde y va de sa petite pique pour expliquer pourquoi ce navigateur est obsolète et pourquoi il ne faut pas le télécharger. [Comme je l'ai déjà expliqué](http://nyams.planbweb.com/blog/2009/01/28/internet-explorer-8-debarque-enfin/ "Internet Explorer 8 débarque enfin") je ne suis pas un défenseur aveugle du dernier navigateur _made in_ Redmond mais de là à déconseiller son téléchargement, il y a là, un pas que je ne franchirais pas. Et pourtant que lit-on dans la presse ou sur les blogs de nos jours sur IE8 ?

**1\. Ce navigateur ne supporte pas HTML5.** J'ai envie de répondre, mais quel navigateur supporte le HTML5 ? Firefox, Safari, Opera ? Même dans leur version de développement ne supporte pas complètement le HTML5 alors pourquoi IE8 devrait être l'exception ? Oui IE8 ne supporte pas les balises `canvas` et les nouvelles balises _media_ (`video` et `audio`) et alors ? Ce n'est pas comme si la non présence de ces balises embêtait l'utilisateur de base lorsqu'il surfe sur le net. Ces balises que je le veuille ou non ne sont pas capitales.

**2\.** **Ce navigateur ne supporte pas le CSS3 même des propriétés comme l'opacité ou les bords arrondis.** Certes, cela est dommageable mais encore une fois, qu'elle navigateur peut dire qu'il supporte la majorité des propriété du CSS3. Opera ne supporte pas les bords arrondis, pourtant ce navigateur est réputé pour [son support exceptionnel des propriétés CSS3](http://my.opera.com/dstorey/blog/show.dml/701902 "Upcoming CSS3 support in Opera")!  De plus, le support des bords arrondis via Gecko ou Webkit n'est qu'expérimental. A moins que je ne me trompe, la propriété `border-radius` n'est supporté par aucun navigateur...

**3\. La gestion des évènements en Javascript est pitoyable.** C'est exact, et je m'en pleins quotidiennement quand je code un site. [Mais au lieu de voir le verre à moitié vide](http://www.robertnyman.com/2008/11/04/internet-explorer-8-fix-event-handling-or-dont-release-it/ "Internet Explorer 8 - fix event handling, or don’t release it"), voyons le verre à moitié plein. la IETeam n'a pas modifié le comportement de son navigateur donc, les _hack_ d'hier continuerons de fonctionner aujourd'hui!!

Les arguments que je viens de citer émanent généralement de ce que j'appelle les **power users**, des utilisateurs qui savent comment fonctionne le web. Au lieu de se plaindre chez Microsoft, il se plaignent chez l'utilisateur final, comme si celui-ci avait  la connaissance et/ou le pouvoir suffisant pour changer la politique de Redmond. IE n'est pas un logiciel libre, l'auriez-vous oublié ?

Pour les néophytes ou les utilisateurs plus alertes qui désirent se renseigner dans la presse dite générale ou sur des sites plus spécialisés essayant d'expliquer à monsieur tout le monde pourquoi IE8 est mauvais ou plutôt obsolète avant même sa sortie :) , on retrouve les arguments suivants :

**[![IE8 ne passe pas l'Acid Test 3](images/ie8acid3-150x150.png "IE8 ne passe pas l'Acid Test 3")](http://www.nyamsprod.com/blog/wp-content/uploads/2009/03/ie8acid3.png)4\. IE8 ne passe pas l'Acid Test 3. ** La version courte de ma réponse serait... **mais on s'en fout de ce putain de test!!!** La version élaborée est de dire que l'[Acid Test 3](http://acid3.acidtests.org/ "Le test Acid pour vérifier des fonctionnalité avancées dans certains domaines des navigateurs") n'est qu'un test parmi une pléthore de tests qui servent à juger de la qualité d'un navigateur. Raté un test ne signifie pas que l'on a raté son examen. C'est comme dire que parce que la voiture que je viens d'acheter possède un lecteur CD incapable de lire des CD au formats _ogg_ ma voiture est obsolète. Non seulement c'est idiot, mais c'est faux!!!

**5\. IE8 est plus lent que les autres navigateurs d'ailleurs il arrive bon dernier dans le test XXX.** Ce que je viens d'expliquer pour le point précédent reste vrai pour ce dernier point. De plus, ce que ce genre d'argument semble ignorer intentionnellement, ou pas, que la vitesse de rendu d'un site sur le net, ne dépend pas uniquement du navigateur mais également de votre connexion, de la bande passante, du chargement du javascript, du DOM dans le navigateur, des images et de l'interaction avec les éléments multimédia de la page (flash, silverlight etc...), de la puissance de votre ordinateur et j'en passe. Bref, un navigateur c'est un tout et il faut réellement se méfiait des résultats des tests de vitesse dans un navigateur.

En résumé ? **Que veut savoir un utilisateur quand on lui propose de mettre à jour un logiciel**, quel qu'il soit ?

1. Est-ce que je continuerai à pouvoir l'utiliser comme son ancienne version ?
2. Est-ce que les différences seront intuitives et est-ce que le temps d'adaptation sera rapide ou non ?
3. Est-ce que je peux mettre à jour le logiciel sans avoir de problème de validation de mon logiciel, de mon OS ?

Vous avez remarqué, je n'ai pas parlé de sécurité, je n'ai pas parlé des nouvelles fonctionnalités apportées par IE8 et surtout je n'ai pas parlé de termes techniques car si il y a bien une chose que j'ai appris .. c'est que l'utilisateur moyen se fout royalement de ce que fait, ou ne fait pas, son navigateur. Il veut simplement qu'il fonctionne et qu'il puisse consulter facilement son compte facebook au bureau :) . A nous webdeveloppeurs de faire de son rêve une réalité!!
