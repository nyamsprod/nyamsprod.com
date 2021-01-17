---
layout: post
title: "Emuler target=\"_blank\" avec javascript, mon howto"
date: "2007-11-30"
categories: 
  - "web"
tags: 
  - "astuce"
  - "dom"
  - "html"
  - "javascript"
---

J'ai décidé d'améliorer mon code d'ouverture d'une page externe à mon site. Pour cela j'ai un peu googlé et surtout je me suis souvenu des fondamentaux du Javascript, souvent cela aide. Essayons donc de résoudre à nouveau le vieux problème de la disparition de l’élément `target` de la spécification XHTML 1.0 Strict. En attendant sa réhabilitation via le [HTML 5.0](http://www.whatwg.org/specs/web-apps/current-work/multipage/ "Le Draft du HTML 5.0"), il existe de nombreuses techniques pour simuler le fameux `target="_blank"` qui manque dans le XHTML, voici ma solution et, surtout le raisonnement que j'ai suivi pour atteindre mon code final.

### Etape 0 : _Que désire-t-on faire exactement ?_

Le principe général de résolution du problème est toujours le même :

1. On récupére tous les liens d’une page;
2. On détermine d’une manière ou d’une autre si le lien pointe vers l’extérieur ou vers l’intérieur du site;
3. Si le lien pointe hors du site on ouvre le lien dans une nouvelle page, et votre visiteur se retrouve sur cette page;
4. Il faut bien sur que le code soit le plus rapide et le plus court possible;

Pour effectuer cela on utilisera le Javascript, car même sans Javascript les liens doivent rester fonctionnels. C’est d’ailleurs l’une des raisons pour laquelle `target` a été enlevé des spécifications du XHTML Strict, car `target` n’avait aucune signification hors des navigateurs évolués, par exemple, sur votre téléphone mobile, `target="_blank"` ne sert à rien.

### Etape 1 : _La solution la plus intuitive_

Tout d'abord, on rajoute à **toutes** les balises `<a>` de votre page dont les liens pointent hors de votre site [l’attribut `rel`](http://www.la-grange.net/w3c/html4.01/struct/links.html#adef-rel "la défintion de l'attribut rel et pourquoi il est important") avec la valeur `external`. Ensuite après avoir effectuer se travail fastidieux, il vous suffira d'ajouter le script suivant à votre page.

\[sourcecode language="javascript"\]var external; var externalLinks=function(){ if( !document.getElementsByTagName ){ return; } var anchorList=document.getElementsByTagName('A'); for(var i=0,anchor;anchor=aList\[i\];i++){ if( anchor.getAttribute('rel').indexOf('external')>-1){ anchor.onclick=function(){ external=window.open(this.href,'external'); external.focus(); return false; }; } } }; window.onload=externaLinks;\[/sourcecode\]

Cette solution est fonctionnelle, puisqu'elle reprend fidèlement les 3 points exposés ci-dessus, mais ce code peut et doit être améliorer.

### Etape 2 : _ce que l’XHTML n’a plus, le DOM l'a toujours_

A la différence de l’XHTML, le DOM permet toujours d'utiliser la propriété `target` sur un lien. Nous pouvons donc faire évoluer notre fonction, et dire au revoir à `window.open` et à la variable `external` :

\[sourcecode language="javascript"\]var externalLinks=function(){ if( !document.getElementsByTagName ){ return; } var anchorList=document.getElementsByTagName('A'); for(var i=0,anchor;anchor=anchorList\[i\];i++){ if( anchor.getAttribute('rel').indexOf('external')>-1){ anchor.target='\_blank'; } } }; window.onload=externaLinks;\[/sourcecode\]

Nous avons amélioré notre script, les pages s’ouvriront alors comme attendues. Une recherche sur le net vous fera invariablement tomber sur une variante de ce script, c’est cette fonction qui est le plus souvent utilisée pour résoudre notre problème.

### Etape 3 : _DOM level 1 ou DOM level 0 que choisir ?_

Le gros point faible des 2 techniques décrites ci-dessus et qu’elles se basent toutes sur des méthodes du `[DOM level 1](http://nyamsprod.com/tutorial/dom/ "un tutorial sur le DOM level 1")` `getElementsByTagName` et `getAttribute`. Si on possède un navigateur qui ne gère pas ce niveau de `DOM` on est un peu, voire beaucoup à la ramasse, de plus , et c'est le plus important ces méthodes sont relativement lentes. Qu’à cela ne tienne, en lisant les spécifications du DOM level 0 j’ai ressorti du congélateur `document.links` l’objet qui gère les liens en `DOM level 0`, notre script devient alors :

\[sourcecode language="javascript"\]var externalLinks=function(){ var anchorList=document.links; for(var i=0,anchor;anchor=anchorList\[i\];i++){ if( anchor.rel.indexOf('external')>-1){ anchor.target='\_blank'; } } }; window.onload=externaLinks;\[/sourcecode\]

Et voilà, maintenant mon script fonctionnera même sous Netscape 4/IE 4. Le script est donc devenu `DOM level 1` Indépendant et il a gagné en rapidité.

### Etape 4 : _window.location à la rescousse_

Continuons à parcourir la classe `document.links`. Certaines de ses propriétés et de ses méthodes sont identiques à ceux de la classe [`window.location`](/qsparser.html "les propriétés et les méthodes de la classe window.location"). Grâce à cela on peut donc obtenir pour chaque lien des informations détaillées sur le domaine pointé, donc l'obligation de récupérer l’attribut `rel` n'est plus de mise, si le domaine du lien est différent du domaine sur lequel se trouve la page qui appelle le script alors on ouvre une nouvelle fenetre, notre script se simplifie encore est devient:

\[sourcecode language="javascript"\]var externalLinks=function(){ var anchorList=document.links; var myhost=window.location.hostname; for(var i=0,anchor;anchor=anchorList\[i\];i++){ if( anchor.hostname != myhost ){ anchor.target='\_blank'; } } }; window.onload=externaLinks;\[/sourcecode\]

Vous vous rappelez le travail fastidieux pour rajouter votre attribut `rel`, et bien grâce à ce nouveau script, vous n’avez plus besoin de le faire. Personnellement je continue à remplir l’attribut `rel`, mais il n’est plus obligatoire pour notre script.

Noter que pour accélérer mon script je déclare 2 variables `anchorLinks` et `myhost`. Si je fais cela c'est pour cacher les résultats de `document.links` et de `window.location.hostname`. Ces variables permettent au navigateur de ne pas recalculer les propriétés de ces classes à chaque itération dans la boucle `for`. J'augmente ainsi la rapidité de mon script.

### Etape 5 : _bye bye window.onload_

Maintenant que notre fonction `externalLinks` est fonctionnelle et optimisée pour tout navigateur qui connait au moins `document.links` et `window.location`, occupons-nous de son éxécution par le navigateur et donc de `window.onload`. Cette méthode de la classe `window` permet d’activer notre fonction quand la page termine le chargement de tous les objets multimédia dont elle a besoin, hors cela représente un double handicap. Si vous avez dans votre page une autre fonction qui est également déclenchée par `window.onload` il y aura conflit entre vos fonctions. Un moyen de contourner ce premier problème est d’utiliser la fonction [`addLoadEvent` de Simon Willinson](http://simonwillison.net/2004/May/26/addLoadEvent/ "l'article de base de la fonction") , mais cela ne fait que déplacer le problème. Si notre document contient beaucoup d’objets à charger, vous serez dépendant du temps de chargement total de ces objets avant que la fonction ne s’active. Dans certains cas le visiteur pourrait même déjà cliquer sur vos liens externes alors que votre script n’a pas encore tourner, donc `window.onload` ne répond pas nos besoins. Une autre solution serait d’utiliser la fonction [`DOMloaded` de Dean Edwards](http://dean.edwards.name/weblog/2005/09/busted/ "l'histoire de DOMloaded commence ici") qui permet de lancer notre fonction dès la fin du chargement de l’arbre DOM dans la mémoire du navigateur. Mais cette fonction dépend partiellement du DOM level 2, donc notre code perdrait en portabilité, donc cette solution est également à abandonner. Finalement on peut tout simplement **placer notre script en fin de page** juste avant la balise de fermeture de `body` et demander son éxecution directe. Ce qui nous donne le code suivant à placer en fin de page :

\[sourcecode language="javascript"\]var externalLinks=function(){ var anchorList=document.links; var myhost=window.location.hostname; for(var i=0,anchor;anchor=anchorList\[i\];i++){ if( anchor.hostname != myhost ){ anchor.target='\_blank'; } } }; externalLinks();\[/sourcecode\]

### Etape 6 : _Javascript c'est magnifique_

J'aurais pu m'arréter là, mais la recherche d'encore plus d'efficacité me faire me rappeler [la définition de la boucle for](http://developer.mozilla.org/fr/docs/Guide_JavaScript_1.5:Boucles:L'instruction_for "Ce que l'on peut faire avec la boucle for en Javascript") en Javascript et cela me permet d'initialiser nos variables directement dans la boucle, de plus je connais une manière d’exécuter le Javascript de façon direct en utilisant le [Block Scope](http://weblog.raganwald.com/2007/08/block-structured-javascript.html "le Block Scope Expliqué"). l'utilisation de toutes ces techniques me permet d'encore plus modifier mon code d'invocation qui devient dès lors :

\[sourcecode language="javascript"\](function(){ for(var anchorList=document.links,myhost=window.location.hostname,i=0,anchor;anchor=anchorList\[i\];i++){ if(anchor.hostname!=myhost){ anchor.target='\_blank'; } } })();\[/sourcecode\]

Et si on diminue la longueur des noms des variables et on met tout sur une ligne on obtient in fine:

\[sourcecode language="javascript"\](function(){for(var l=document.links,h=window.location.hostname,i=0,a;a=l\[i\];i++){if(a.hostname!=h){a.target='\_blank';}}})();\[/sourcecode\]

et voila… :) vous avez devant vous la fonction que j'utilise en ce moment pour mon site. C'est pas magnifique ça !!!
