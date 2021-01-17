---
layout: post
title: "insérer une image en utilisant la balise object"
date: "2009-01-23"
categories: 
  - "web"
tags: 
  - "balise"
  - "html5"
  - "ie8"
  - "image"
  - "insertion"
  - "microformats"
  - "navigateur"
  - "object"
  - "tag"
---

Si il y a bien une balise HTML qui est mal connue, c'est bien la balise `object`. Elle fait partie officiellement du HTML depuis sa version 4 mais, de part le manque de renouvellement d'Internet Explorer pendant 5 ans, son utilisation pour autre chose que l'insertion de contenu Flash dans une page n'a jamais été mise en avant. Un exemple d'utilisation pertinente de la balise `object` peut se faire dans le cadre d'un comic strip . L'un des webcomic que je suis régulièrement est [geeksworld](http://www.geeksworld.org/ "La Vie de Geeks par un Geek") de Salagir. J'ai remarqué que pour permettre une meilleur indexation de son comic, Salagir a eu la bonne idée de retranscrire l'entièreté des bulles de son strip dans la page qui le contient. Ainsi les robots qui vont naviguer sur son site vont non seulement indexer l'image mais également les informations textes qui sont liées celle-ci. pour accomplir cela Salagir a mis au point un script qui [permet d'extraire le texte d'un fichier PSD](http://blog.salagir.com/41-extracteur-de-textes-dun-fichier-photoshop/ "Comment extraire le texte d'un fichier PSD") et il utilise le schéma HTML suivant :

Le texte du strip vient ici

\[sourcecode language="html"\]![](images/image.png)

Le texte du strip vient ici

\[/sourcecode\]

Pour fonctionner correctement, Salagir a donc rajouté la règle `display:none;` pour la balise `div` ayant pour attribut `class="textstrip"`. Cette construction bien que fonctionnant parfaitement ne permet pas d'associer directement le texte à l'image en ce sens que l'image est indépendante du texte et, à moins d'utiliser des _microformats_ spécifiques aux webcomics (je ne sais pas si cela existe...) le lien entre texte et image n'est pas évident. Une solution pour remédier à ce manque de relation serait, dans ce cas, d'insérer l'image en utilisant la balise `<object>`. Comment ? Suivez le guide.

**1ère étape :** on insère l'image en utilisant les recommandations du W3C et la balise `object` : \[sourcecode language="html"\] \[/sourcecode\]

**2ème étape :** on ajoute le texte correspondant au webcomic à l'intérieur de la balise `object :` \[sourcecode language="html"\]

Le texte du strip vient ici

\[/sourcecode\]

Vérifions [si cela fonctionne bien](http://nyamsprod.com/test/salagir/w3c.html "Utilisation de la balise Object pour insérer une image") sous tous les navigateurs récents ?

- **La bonne nouvelle** et que cette construction fonctionne parfaitement dans tous les navigateur récents, y compris Internet Explorer 8. Le texte encapsulé dans le tag `object` n'apparaît pas mais peut toujours être parser par les robots des différents moteurs de recherche.
- **La mauvaise nouvelle** c'est que toutes les anciennes versions de IE, y compris IE7, se comportent différemment des recommendations du W3C, et montre l'image dans une boite avec l'apparition d'une échelle (scroller).

Mais cela n'est pas grave en utilisant les [commentaires conditionnels de IE](http://msdn.microsoft.com/en-us/library/ms537512.aspx "Tous ce qu'il faut savoi des commentaires conditionnels sous IE"), on peut obtenir le même résultat dans les versions antérieurs à Internet Explorer 8. Ce qui nous donne [un résultat fonctionnel sous tous les navigateurs](http://nyamsprod.com/test/salagir/ "Affichage cross-navigateurs du comic strip"). Etudier bien la source du fichier pour comprendre l'astuce utilisée.

L'étape ultime serait [d'utiliser la balise `dialog` de HTML5 ou les microformats](http://www.nikhilk.net/HTML5-Dialog-Microformats.aspx "HTML5 ou Microformat que choisir ?") pour encore mieux formaliser les dialogues du strip. Mais ça c'est une autre histoire. Que pensez-vous de cette solution ?

_Je remercie Salagir, pour m'avoir permis d'utiliser son strip._
