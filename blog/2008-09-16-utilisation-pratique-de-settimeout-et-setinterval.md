---
title: "utilisation pratique de setTimeout et setInterval"
date: "2008-09-16"
categories: 
  - "web"
tags: 
  - "astuce"
  - "closures"
  - "eval"
  - "firefox"
  - "internet-explorer"
  - "javascript"
  - "opera"
  - "safari"
  - "setinterval"
  - "settimeout"
---

En javascript, comme dans tous les langages de script et/ou de programmation, il existe des fonctions plus "puissantes" que d'autres et dont [l'utilisation doit être faite avec beaucoup de précautions](http://ejohn.org/blog/eval-kerfuffle/ "Eval c'est le mal"). Deux de ces fonctions dont la puissance et/ou la mauvaise utilisation peuvent aboutir à un crash de votre navigateur sont `setTimeout` et `setInterval`. C'est pourquoi à chaque nouvelle mouture de la langue, les concepteurs des différents navigateurs essaient d'en contrôler voire d'en diminuer les effets néfastes possibles.

Récemment j'ai du coder un effet de carrousel pour un site. Le code n'est d'ailleurs pas totalement fini, mais là n'est pas le propos. Afin de créer l'illusion de carrousel, j'ai eu recours à la fonction `setTimeout` et pour l'utiliser comme il se doit, j'ai eu recours à la documentation du [Mozilla Developper Center](http://developer.mozilla.org/fr/DOM/window.setTimeout "setTimeout tel que implanté sous Firefox, Safari et Opera"). Selon cette documentation `setTimeout` comme `setInterval` peuvent prendre jusqu'à 255 arguments dont :

- le nom d'une fonction ou une chaîne de caractères, évaluée en javascript via la fonction `eval`, comme 1er argument ;
- le temps minimum qui doit s'écouler entre 2 appels à la fonction, comme 2ème argument ;
- une liste d'arguments qui seront automatiquement appelés par la fonction indiquée dans le premier argument.

De fait mon appel à setTimeout ressemblait à ceux-là :

\[sourcecode language="javascript"\]var animate = function() {
    var x;
    return function (o, start, stop, dist) {
        o.style.left = start;
        if( stop > start ){
            start += dist;
            x = setTimeout(arguments.callee, interval, o, start , stop, dist );
        } else {
            clearTimeout(x);
        }
    };
}();
/\*
arguments.callee représente l'appel récursif à la fonction animate 
o représente l'objet DOM auquel j'applique le "mouvement"
start la position qu'il doit prendre
interval le temps qui s'écoule entre 2 appels à la fonction
stop la position finale
dist la distance a parcourir entre chaque appel à la fonction
\*/\[/sourcecode\]

Tout fonctionnait très bien sous Firefox, Safari et Opera, mais lorsque j'ai du finalement tester le code sous Internet Explorer, tada, surprise :) , mon code ne fonctionnait plus. N'arrivant pas à savoir pourquoi, après avoir essayer de corriger mon code sans succès, j'ai décidé de consulter [la documentation fournie par Microsoft de `setTimeout`](http://msdn.microsoft.com/en-us/library/ms536753.aspx "setTimeout tel que implanté sous Internet Explorer") et que vois-je ? les fonctions `setInterval` comme `setTimeout` ne peuvent prendre que 3 paramètres, sous Internet Explorer. **le troisième argument indiquant si on est en Jscript, en VBscript ou en Javascript.** La seule manière de résoudre mon problème a donc été d'utiliser les _closures_ et de rendre toutes mes variables globales. Bref beaucoup de concept dont on ce serait bien passé, ce qui me donne la solution suivante :

\[sourcecode language="javascript"\]var animate = function (){
    var o, start, stop, dist, x;
    var \_animate = function() {
        o.style.left = start;
        if( stop > start ){
            start += dist;
            x = setTimeout(arguments.callee, interval);
        } else {
            clearTimeout(x);
        }
    };
    return function(el, begin, end, delta){
        o = el;
        start = end;
        dist = delta;
        \_animate();
    };
}();\[/sourcecode\]

Aux developpeurs de IE8, essayez de corriger le tir car plus personne n'utilise Jscript ou VBscript sur le net. Et cela nous permettra, à nous, développeurs de ne pas avoir à recourir a des solutions qui alourdissent inutilement le code et le rende rapidement illisible ;) . en écrivant ce poste je suis tombé [sur cette solution](http://webreflection.blogspot.com/2007/06/simple-settimeout-setinterval-extra.html "Comment résoudre le problème avec des commentaires conditionnels") mais vu que je ne l'ai pas encore testé, je vous laisse juge de son efficacité.
