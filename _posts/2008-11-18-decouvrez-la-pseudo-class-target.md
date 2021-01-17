---
layout: post
title: "Découvrez la pseudo class :target"
date: "2008-11-18"
categories: 
  - "web"
tags: 
  - "css"
  - "css-3"
  - "internet-explorer"
  - "pseudo-class"
  - "target"
  - "trident"
---

[](http://www.nyamsprod.com/blog/wp-content/uploads/2008/11/pseudo_class_target_before.png)Comme chaque année plus ou moins à la même période, je change/fais évoluer le thème de mon site. Cette année, profitant des nouvelles fonctionnalités déjà et/ou bitentôt disponibles dans les moteurs de rendu des navigateurs, j'ai décidé de faire la part belle aux propriétés du CSS3, même celles qui sont encore à l'état de draft. Parmi toutes les propriétés que j'ai retenues, il y en a une que j'ai trouvée géniale,  sans doute parce que je ne l'ai découverte **que** la semaine dernière, par hasard, en relisant les normes du W3C à la recherche de tout à fait autre chose. 

Cette propriété c'est la pseudo class `target`. Que les choses soient bien claires dans votre esprit, cette pseudo class CSS n'a rien à voir avec [l'attribut target des balises de références](http://nyamsprod.com/blog/2007/11/30/optimisation-de-mon-code-javascript-pour-emuler-target_blank/ "Emuler target blank"). Non, en revanche, elle est utilisée pour modifier le CSS de l'élément vers lequel pointe une url.... hein? késako !? Okay je reprends ma phrase en essayant de me faire mieux comprendre :

Soit un lien du type `http://www.example.com/index.html#toto` , si la page `index.html` contient bien une balise avec pour `id="toto"`, en utilisant la pseudo class `:target` sur cet élément on peut modifier ses propriétés CSS lorsque le navigateur pointe sur lui... okay ça va vous comprenez toujours pas, c'est normal, c'est difficile à expliquer et comme un exemple vaut mieux qu'un long, incompréhensible et ennuyeux discours [voici ce que vous devriez voir](http://nyamsprod.com/test/target/w3c.html "la pseudo class target en action") en cliquant sur le lien test1 :

[![](images/pseudo_class_target_before-300x154.png "pseudo_class_target_before")](http://www.nyamsprod.com/blog/wp-content/uploads/2008/11/pseudo_class_target_before.png "utilisation rudimentaire de la pseudo class target avant le clic sur le lien test1") [![](images/pseud_class_target-300x166.png "utilisation rudimentaire de la pseudo class target")](http://www.nyamsprod.com/blog/wp-content/uploads/2008/11/pseud_class_target.png "utilisation rudimentaire de la pseudo class target après le clic sur le lien test1")

Et pour obtenir ce résultat quelque ligne CSS suffisent, à vrai dire il en faut uniquement 2!! : \[sourcecode language="javascript"\]td { vertical-align:top; border:3px solid #000; } td:target { background-color:#ffcc33; color:#f00; }\[/sourcecode\] Ce qui est géniale avec cette propriété c'est qu'elle est déjà incluses dans tous les grands moteurs de rendu, à l'exception, bien évidemment de Trident (_Internet Explorer_). Et, hélas, IE8 ne supportera pas cette méthode. Mais cela n'est pas un grand problème en soit, ce que CSS ne peut faire... [javascript sait et peut le faire](http://nyamsprod.com/test/target/index.html "Utilisation de javascript pour émuler la pseudo class :target") (oui j'ai le droit d'utiliser le verbe _savoir_ Maxime :D ) . C'est, d'ailleurs, en utilisant cette technique de manière beaucoup plus évoluée que j'ai pu mettre au point le nouveau menu du site, toute l'idée est là. Je suis sûr que des designers plus talentueux que moi réussiront [à faire beaucoup mieux](http://virtuelvis.com/gallery/css3/target/interface.html "Utilisation plus évoluées de la pseudo class :target") , mais j'aurais au moins le mérite d'avoir tenter quelque chose ;) . Et vous vous en pensez quoi de cette pseudo classe ?
