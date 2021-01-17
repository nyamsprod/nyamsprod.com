---
layout: post
title: "parcourir un document web en utilisant le DOM"
date: "2009-01-21"
categories: 
  - "web"
tags: 
  - "chrome"
  - "filter"
  - "firefox"
  - "foreach"
  - "getelementbyid"
  - "getelementsbytagname"
  - "ie8"
  - "opera"
  - "queryselector"
  - "queryselectorall"
  - "safari"
  - "v8"
  - "webkit"
---

Pendant des années, la vie quotidienne des développeurs web, lorsqu'ils travaillaient avec le DOM, se résumait en l'utilisation de la boucle `for` avec les méthodes [`getElementById`](http://nyamsprod.com/tutorial-dom-04.html "Utilisation de getElementById") et [`getElementsByTagName`](http://nyamsprod.com/tutorial-dom-06.html "Utilisation de getElementsByTagName") pour récupérer tel ou tel balise du HTML. Mais tout cela est fini (enfin!!), remontons le temps pour voir ce que l'on faisait avant et ce que l'on fera demain :) .

Le problème qui ce pose est toujours de ce type :

> Comment sélectionner toutes les balises enfants de type liste inclue dans mes balises `div` avec la `class="post"` enfants d'une balise `div` ayant pour `id="content"`.

Avec la sortie du DOM1, la solution à ce problème fut le code suivant :

\[sourcecode language='javascript'\]var nodeList = document.getElementById('content').getElementsByTagName('div'); var res = \[\]; for (var i = 0, div; div = nodeList\[i\]; i++) { if (/(^|s)post(s|$)/.test(div.className)) { if (div.hasChildNodes) { for (var j = 0, o; o = div.childNodes\[j\]; j++) { if(/^(UL|OL|DL)$/.test(o.nodeName)) { res\[res.length\] = o; } } } } }\[/sourcecode\]

Avec l'avènement de Firefox 1.5 est [des méthodes avancées de manipulation des tableaux](https://developer.mozilla.org/fr/Nouveaut%C3%A9s_dans_JavaScript_1.6 "Toutes les méthodes avancées de manipulations des tableaux dans Firefox"), le code s'est "simplifié" de la sorte

\[sourcecode language="javascript"\]var res = \[\]; var nodeList = Array.filter(document.getElementById('content').getElementsByClassName('post'), function (el) { return(el.nodeName==='DIV'&&el.hasChildNodes); }); if (nodeList.length>0) { Array.forEach(nodeList, function (el) { var r = Array.filter(el.childNodes, function (el) { return /^(UL|OL|DL)$/.test(el.nodeName); }); if (r.length > 0) { res = res.concat(r); } }); }\[/sourcecode\]

Mais seul, Firefox comprend, nativement le code ci-dessus, et bien que plus simple (il n'y a plus de boucle `for`), l'écriture d'un tel code est en fait plus difficile. Depuis, les différentes framework javascript on mis en place toute une série de méthodes aux noms variés pour remédier à cette complexification. Mais tous cela, c'est du passé grâce à `querySelectorAll` on aura désormais plus qu'à écrire ceci :

\[sourcecode language="javascript"\]var res = document.querySelectorAll("#content div.post > dl, #content div.post > ul, #content div.post > ol");\[/sourcecode\]

[Essayez ces scripts dans différents navigateurs](http://nyamsprod.com/test/domtraverse/ "Test des Scripts proposés : En fonction de votre navigateur, l'un ou l'autre script sera utilisée") et vous verrez par vous-même que cela donne la même réponse.

**Première bonne nouvelle :** `[querySelectorAll](http://msdn.microsoft.com/en-us/library/cc288326(VS.85).aspx "Documentation de querySelectorAll pour Internet Explorer 8")` permet de faire des recherches en utilisant une déclaration CSS à la manière de différentes frameworks javascript **mais** diffère de celles-ci en cela qu'elle retourne une liste de noeud et reste strict par rapport au règles du CSS. C'est donc une version modernisée de `getElementsByTagName`. De même [`querySelector`](https://developer.mozilla.org/En/DOM/Document.querySelector "Comment fonctionne querySelector selon Mozilla") fonctionne exactement comme `querySelectorAll` **mais** ne renvoie que le premier noeud qui satisfait à la condition CSS, c'est donc l'équivalent moderne de `getElementById`.

**Deuxième nouvelle :** La rapidité de ces fonctions, native dans le navigateur, nous permettra d'avoir des script beaucoup plus rapide

**Troisième bonne nouvelle :** Cette année 2009 verra la mise à jour de minimum 3 grands navigateurs, IE passera la 8ème vitesse, Firefox fera un toilettage de sa mouture avec une version 3.1 très attendue, quand à Opera il a déjà annoncé les couleurs avec une version alpha de son prochain navigateur Opera 10. De toute les nouveautés qui nous attendent avec l'arrivée de ces différents navigateurs une est de taille, le support par tout les navigateurs modernes de ces méthodes `querySelector` et `querySelectorAll`, qui sont déjà présentent sous Safari depuis sa version 3.1. Bref 2009 s'annonce comme un bon cru pour le DOM et le Javascript.
