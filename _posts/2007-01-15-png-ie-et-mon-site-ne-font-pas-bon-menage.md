---
layout: post
title: "PNG, IE, et mon site ne font pas bon ménage"
date: "2007-01-15"
categories: 
  - "web"
tags: 
  - "bug"
  - "internet-explorer"
  - "navigateurs"
  - "png"
  - "transparence"
---

**Attention** : [une mise à jour de cet article a était publié](http://nyamsprod.com/blog/2007/12/09/png-ie-et-mon-site-ne-font-pas-bon-menage-mise-a-jour/ "PNG, IE, et mon site ne font pas bon ménage - mise à jour"), le 19 Décembre 2007, avec l'explication complète du bug.

#### I.Le constat

Pendant la mise à jour de mon site j'ai changé le logo de mon site et comme, je suis pas très futé; je suis allé sur le net pour trouver de l'inspiration et des tutoriaux pour [créer mon nouveau logo](http://www.fxdesigning.com/web2txt.php "Tutoriel pour  créer un logo 2.0"). Au momment de sauver mon nouveau logo, Photoshop m'a proposé 3 types de fichier : `GIF` ,`JPEG` et `PNG`. Suivant les [recommendations sur le type de fichier à choisir](http://www.yourtotalsite.com/archives/miscellaneous/which_image_format_is_bes/ "comment choisir le format d'image pour votre site") j'ai sauvé mon logo en `PNG`. Le résultat fut alors assez étrange dans le navigateur que tous le monde adore, Internet Explorer et ce, quelque soit la version.

<table border="0" summary="illustration du bug de rendu d'une image au format PNG sous Internet Explorer"><tbody><tr><td><h4>Internet Explorer</h4></td><td><h4>Dans les autres navigateurs</h4></td></tr><tr><td><p style="text-align: center"><img title="la partie de mon header sous Internet Explorer" src="images/png_bug_ie.gif" alt=""></p></td><td><p style="text-align: center"><img title="la partie de mon header sous Firefox" src="images/png_bug_ff.gif" alt=""></p></td></tr><tr><td>la couleur de l'arrière plan diffère légèrement de la couleur de fond du logo</td><td>Dans les autres navigateur, on observe aucune différence entre arrière plan et la couleur de fond du logo</td></tr></tbody></table>

#### II.L'explication

Après moultes investigations sur le net. Je retombais toujours sur le même problème de [transparence de PNG](http://support.microsoft.com/kb/294714/fr "gestion de la transparence du PNG sous IE 6") sous IE6. Mais bon là, le problème est le même sous IE7 et [ce bug est censé être résolu pour les PNG](http://blogs.msdn.com/ie/archive/2006/08/22/712830.aspx "Résolution du bug de transparence sous IE7")... **, de plus il n'y a pas de transparence dans mon logo!!!**Une piste serait de dire que [Trident](http://en.wikipedia.org/wiki/Trident_(layout_engine) "Le moteur de rendu de la famille IE") a encore des problème avec le PNG, bug qui ne se limite pas au traitement de la transparence.. à moins que cela soit liés mais je vois pas comment. Bref en attendant, je n'ai pas d'explication solide et comme je suis pas graphiste, je ne peux que constater.

#### III.La solution

En attendant une explication à ce phénomène, j'utilise une expression conditionnel sous IE pour ajuster la couleur de mon arrière plan à la _nouvelle couleur_ de fond de mon image. En espérant que IE 8 règle ce problème une bonne fois pour toute.

<!--\[if IE lt 8\]><style type="text/css" media="screen">#header { background-color:#FFE295; }</style><!\[endif\]-->

Le côté intéressant de cette histoire c'est que j'ai trouvé une nouvelle utilisation pour l'[IE Developper Toolbar](http://www.microsoft.com/downloads/details.aspx?familyid=e59c3964-672d-4511-bb3e-2d5e1db91038&displaylang=en "La barre de WebDev à la sauce IE"), qui m'aide maintenant à déterminer la couleur exact de l'arrière plan de mon image sous IE et ensuite à ajuster la couleur de fond de mon entête comme indiqué ci-dessus.
