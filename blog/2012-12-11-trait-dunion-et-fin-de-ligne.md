---
title: "Trait d'union et fin de ligne"
date: "2012-12-11"
categories: 
  - "web"
tags: 
  - "cesure"
  - "css3"
  - "fin-de-ligne"
  - "hyphen"
  - "responsive-design"
---

A chaque jour son lot de nouveauté dans les navigateur. Aujourd'hui j'apprend que les navigateurs récents (IE10 et Firefox en tête) arrivent à prendre en charge correctement [les traits d'union en fin de ligne](http://www.quirksmode.org/blog/archives/2012/11/hyphenation_wor.html "How to make Hyphenation works in mordern browsers") comme les journaux papiers d'antan. Pour ce faire vous aurez besoin de 2 ingrédients indispensables:

1. un attribut `lang` sur une balise de type block qui permet au navigateur de déterminer la langue du texte utilisé et donc d'appliquer les bonnes règles de césures en fin de ligne;
2. la propriétés CSS qui enclenche l'utilisation des trait d'union et qui s'appelle `hyphen`;

Noter que si vous ne voulez pas vous embétez et que votre site est en une seul langue, il vous suffira d'ajouter l'attribut `lang` à la balise html. Une autre raison donc de ne plus omettre cette attribut la prochaine fois que vous codez un site.

Et hop, un nouvel outil assez sympa pour permettre une meilleur présentation et/ou organisation de vos textes dans un monde ou le Responsive Design devient la norme. D'ailleurs pour les plus chanceux d'entre vous, j'ai adapté la feuille de style principale de mon site pour qu'elle prenne en compte cette propriété ;) .
