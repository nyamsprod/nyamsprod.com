---
title: "Javascript Snippets : Trim"
date: "2010-12-10"
categories: 
  - "web"
tags: 
  - "javascript"
  - "navigateur"
  - "trim"
---

En `javascript`, un développeur est tôt ou tard confronter aux données envoyée par un utilisateur. Hors comme tout le monde le sait il ne faut jamais avoir confiance en un utilisateur. Afin de prévenir les ajouts irréfléchis de ceux-ci une fonction intéressante qui existe dans tous les langages moderne est la fonction `trim`. Celle-ci permet d'enlever le surplus de caractères vides en amont et en aval d'une chaine de caractère soumise.

Mais comme le `Javascript` n'est pas comme tous les langages (si si.. je vous l'assure :) ), jusqu'à très récemment, le langage était dépourvu de fonction native `trim`. Mais tout cela va changer car avec, `EcmaScript 5`, tous les navigateurs récents (y compris IE9) possèdent dorénavant une fonction `trim` en natif. Le code suivant fonctionnera donc désormais sans aucun problème dans votre navigateur.

\[sourcecode language="javascript"\]var my\_string = "   I'm sick of using javascript workaround for the trim function     "; my\_string.trim();  //ce qui donne "I'm sick of using javascript workaround for the trim function"\[/sourcecode\]

Et pour les anciens navigateurs me direz-vous, on fait comment ? Hé bien, c'est simple, un petit code bien ficelé vous permettra d'également utiliser la fonction `trim` sur les vieux navigateurs encore en service. Elle est belle la vie des développeurs quand même ;) .

\[sourcecode language="javascript"\]//ajouter ce code avant d'utiliser la fonction trim bien évidemment if (!String.prototype.trim) { String.prototype.trim = function() { return this.replace(/^ss\*/, '').replace(/ss\*$/, ''); }; }\[/sourcecode\]

_PS: [il existe beaucoup de méthodes pour effecteur cette opération](http://blog.stevenlevithan.com/archives/faster-trim-javascript), celle que j'ai choisi est basé sur le code de [@slevithan](http://www.twitter.com/slevithan)_
