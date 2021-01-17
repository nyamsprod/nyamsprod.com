---
title: "Générer des flux RSS différents pour votre blog avec Wordpress"
date: "2009-02-18"
categories: 
  - "web"
tags: 
  - "atom"
  - "feedburner"
  - "flux"
  - "get_author_feed_link"
  - "get_category_feed_link"
  - "get_tag_feed_link"
  - "html"
  - "php"
  - "rss"
  - "tags"
  - "template"
  - "wordpress"
---

Vous avez mis en place votre blog et maintenant il ne vous reste plus qu'à le diffuser et pour cela rien de plus simple que d'utiliser les flux RSS/Atom pour permettre à vos fans à travers le monde de vous suivre. Mais seulement comment faire ?

Avec Wordpress la gestion des flux RSS/Atom est devenu très simple et s'améliore à chaque version. Lorsque j'ai mis à jour mon thème, ce que j'essaie de faire régulièrement, je me suis posé la question, comment générer et gérer de manière simple des flux différentielles venant de mon blog, et je ne parle pas là, de leur diffusion via un service comme feedburner.

Un billet, un poste, un article, cela dépend de comment vous l'appelez est identifiable selon 4 grands critères dans un blog.

- sa date de parution
- son auteur
- sa catégorie
- ses tags

Ce qui est génial avec Wordpress, c'est que depuis sa version 2.5, il est possible de fournir un flux personnalisé de votre blog à partir de chacun de ces critères et je vais vous dire comment.

_Attention une connaissance des templates Wordpress et du PHP sont des pré requis pour la suite de cette article_

Voici les quelques lignes de codes que vous devrez utiliser pour afficher dans votre template Wordpress le bon flux en fonction de la page/section de votre blog. Noter que pour utiliser à bien ces fonctions, il vous faudra pour chaque type de section de votre blog :

1. déterminer l'identifiant, de la catégorie , de l'auteur et/ou du tag;
2. passer cette identifiant à la fonction adéquate qui générera l'url adéquat du flux recherché;

Si vous êtes en train de surfer dans une section de catégorie, utiliser le code suivant : \[code='php'\]cat\_ID; $rss\_link        = get\_category\_feed\_link($theID); $rss\_description = 'flux RSS de la categorie : ' . single\_cat\_title(); } ?>\[/code\] La méthode mise à notre disposition pour déterminer le lien vers votre flux est `get_category_feed_link.` Si vous êtes sur une page regroupant les postes par tag, le code ci-dessous est plus approprié : \[code='php'\]\[/code\] La méthode mise à notre disposition pour déterminier le lien RSS est `get_tag_feed_link` Enfin pour générer le flux RSS reprenant les postes d'un de vos auteurs, utiliser le code ci-dessous : \[code='php'\]ID); $rss\_description = 'flux RSS  pour : ' . $author->nickname; } ?> \[/code\] La méthode mise à notre disposition pour déterminer le lien RSS est `get_author_feed_link` Afin d'être exhaustif, je reprends ici le cas le plus général, le flux de votre site en fonction de la date de parution de vos billets : \[code='php'\]\[/code\]

Par défaut, vos flux seront du type RSS 2.0, mais ne vous inquiétez pas, pour obtenir des flux de type _Atom_ il suffit d'indiquer en deuxième argument de chacune des fonctions décrites ci-dessus le mot _'atom'_ et le tour est jouer ;) .

Un manière simple d'inclure le résultat dans le template de votre blog serait d'utiliser le code suivant à l'endroit.

\[code='php'\][](<?php echo $rss_link ?>)\[/code\]

Les méthodes décrites ci-dessus existent depuis la version 2.5 de Wordpress, mais comme elles sont peu documentées, les plus malins d'entre-vous qui ne les connaissent pas (j'ai fait partie de ces malins pendant longtemps :) ) rajoutent simplement le code `/feed/` en fin d'URL de ces différentes sections pour obtenir le même résultat.

L'avantage de ces méthodes par rapport à l'ajout de suffixe `/feed/` et qu'elle ne nécessite pas la connaissance à priori de la syntaxe utilisée pour générer les liens dans Wordpress.
