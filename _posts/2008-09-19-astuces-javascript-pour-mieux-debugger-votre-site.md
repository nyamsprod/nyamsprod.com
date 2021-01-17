---
layout: post
title: "Astuces Javascript pour mieux débugger votre site"
date: "2008-09-19"
categories: 
  - "web"
tags: 
  - "astuce"
  - "css"
  - "debugger"
  - "html"
  - "javascript"
  - "librairie-javascript"
  - "webdesign"
---

Quelque soit votre niveau de connaissance en CSS ou en javascript, en tant que développeur, vous vous êtes sûrement retrouvés devant le cas où vous deviez recharger votre site pour observer le résultat de vos modifications. Et bien voici un script javascript simple qui va vous faciliter la vie.

![](images/gift_surprise-300x300.jpg "gift_surprise")[Quelque](http://getfirebug.com/ "Firebug, la Rolls Royce du Debug") [soit](http://www.opera.com/products/dragonfly/ "Le Debug vue par l'équipe d'Opera") [l'outil](http://regagnon.com/blog/2008/02/10/debloquer-le-menu-debug-sous-safari/ "Débloquer le menu de Debug sous Safari") [performant](http://blogs.msdn.com/ie/archive/2008/09/11/introducing-the-ie8-developer-tools-jscript-profiler.aspx "Internet Explorer 8 ne restera pas sur la touche pour le debug") que vous utilisez pour corriger vos bugs, in fine, pour pouvoir observer le résultat de vos diverses corrections et améliorations, vous êtes obligés de recharger votre page pour récupérer les versions les plus récentes de vos scripts. En re-lisant [mon didactitiel sur le javascript](http://nyamsprod.com/tutorial-dom-13.html "Comment changer le CSS d'une page en utilisant le DOM"), une idée simple m'a traversé l'esprit. Et si, au lieu de toujours recharger ma page entière, comprenant le HTML, le CSS et le javascript,  je ne chargeais que les fichiers qui ont été modifiés , c'est-à-dire, les scripts javascript et/ou les feuilles de style externes. Cela me permettrait de voir la mise à jour de ma page sans avoir à la recharger complètement, une perspective intéressante si vous êtes en train de coder une application Ajax, par exemple. Donc après une petite réflexion de 5 minutes et un codage encore plus rapide, je vous présente le code qui va vous permettre de **recharger les scripts et les feuilles de style externes d'une page web**. C'est tellement simple et efficace que je me demande si quelqu'un n'a pas déjà eu cette idée sur le net :) .

\[sourcecode language='javascript'\]//CSS reload
var reloadCSS = function() {
   var l = document.getElementsByTagName('link');
   var t = new Date().getTime();
   var o, a;
   for (var i = 0; o = l\[i\]; i += 1) {
        if (/stylesheet/i.test(o.rel) && o.href) { //si c'est une feuille de style
            a = o.href.replace(/(&|?)timestamp=d+/, '');
            o.href = a + (a.indexOf('?') === -1 ? '?' : '&') + 'timestamp=' + t;
        }
    }
};

//Javascript reload
var reloadJS = function() {
   var l = document.getElementsByTagName('script'); 
   var t = new Date().getTime();
   var o, a;
    for (var i = 0; o = l\[i\]; i += 1) {
        if (/javascript/i.test(o.type) && o.src) { //si c'est un javascript
            a = o.src.replace(/(&|?)timestamp=d+/, '');
            o.src = a + (a.indexOf('?') === -1 ? '?' : '&') + 'timestamp=' + t;
        }
    }
};\[/sourcecode\]

Il ne nous reste plus qu'à rajouter dans notre page un lien ou une balise qui permettra d'appeler nos fonctions comme suit :

\[sourcecode language='javascript'\]
\[/sourcecode\]

Et voila!!! **Bien sûr, une fois en production, vous n'oublierez pas de commenter les boutons** pour les ré-utiliser au moindre debug, on ne sait jamais ;) .

- _A noter, le dernier bouton permet via un appel unique de mettre à jour le CSS et le Javascript externe de votre page/site_.
- _Pour que le script `reloadJS` fonctionne il faut que votre balise `script` contienne l'attribut `type` avec la valeur recommandée par le W3C._
