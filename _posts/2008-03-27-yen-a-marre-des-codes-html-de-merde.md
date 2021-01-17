---
layout: post
title: "Y'en a marre des codes html de merde!!"
date: "2008-03-27"
categories: 
  - "web"
tags: 
  - "amateurs"
  - "boulets"
  - "codeurs"
  - "coup-de-gueule"
  - "dom"
  - "html"
  - "yen-a-marre"
---

On est en Mars 2008 et je poste mon premier vrai coup de gueule. Celui-ci est adressé aux soit disant designers, développeurs web qui se disent être des professionnels. Y'en a marre des codes javascript de merde que je rencontre dans les design _html_ que je commande chez de tels individus. J'en ai marre des liens html du type : \[sourcecode language="html"\][cliquez ici!!](javascript:void(0);)\[/sourcecode\] Franchement, je me demande pourquoi on se fait chier à écrire des recommandations ou [des tutoriels](http://nyamsprod.com/tutorial-xhtml-00.html "Un tutoriel sur le XHTML"), pourquoi on s'évertue à [indiquer aux constructeurs de navigateurs les bugs](http://www.quirksmode.org/bugreports/index.html "Quirksmode consacre une partie de son site au bugs report") que l'on rencontre, si nous même, en 2008 on n'est pas capable d'écrire un lien _html_ avec la bonne syntaxe _javascript_ qui va bien. C'est vrai quoi, avec tous les bons sites de référence sur le net, le designer avec lequel je bosse sur un projet m'a pondu le code ci-dessus sans sourciller. _Pour des raisons de déontologie, le code exact a été légèrement retouché_ ;) . Finalement je crois que je vais faire comme [Dustin Diaz](http://www.dustindiaz.com/web-1-point-oh-techniques/ "Les nouvelles techniques du web qui vont tous révolutionnées") et choisir d'en rire.

Récapitulons rapidement les erreurs de ce code :

1. [**`javascript:void(0);`**](http://www.quirksmode.org/blog/archives/2005/06/three_javascrip_1.html "Comment bien écrire le javascript dans un lien") : un pourriture qui date de l'aube du html et qui aurait du être enterré en même temps que Netscape 4.0 au minimum;
2. [**La présence de `onclick` avec 1 C majuscule** :](http://nyamsprod.com/tutorial-xhtml-02.html "les bases et fondements du XHTML") c'est vrai je ne l'ai pas dis mais ce lien m'a était livré avec une DTD certifiant que mon document était du type XHTML 1.0;
3. **cliquez-ici** : l'utilisation de ces mots certifiés _Web 0.1 beta 3_ pour indiquer un lien m'énerve au plus haut point. Si c'est un lien et c'est le cas, c'est pas pour faire joli, c'est pour qu'on clique dessus, donc comme cela coule de source pas la peine d'en rajouter ;
4. Si pour une raison X ou Y , le javascript ne fonctionne pas dans le navigateur qui va exécuter ce code, hé bien rien ne se passera lorsque l'on cliquera sur le lien , c'est con n'est pas;
5. [L'oubli de **`return false`** **dans le onclick**](http://www.quirksmode.org/js/events_early.html "Explication du pourquoi du comment qu'il faut ajouter return false") : Si un lien est définit dans l'attribut `href`, se lien sera de toute manière suivie avec le javascript activé;

Et oui, en moins d'une ligne de _html/javascript_ autant d'erreurs commises par un newbie, boulet, codeur du dimanche ne m'aurais pas fait broncher, mais venant d'une personne payée pour coder et livrer un travail dit professionnel, je trouve cela totalement inacceptable. Je n'y résiste tout de même pas et je vous livre le code revu et corrigé pour la paix de vos âmes :

<a href="http://www.amazina.com" onclick="openthis(this.href); return false">amazina</a>

A bon entendeur salut.
