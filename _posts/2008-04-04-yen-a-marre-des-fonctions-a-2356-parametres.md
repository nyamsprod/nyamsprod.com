---
layout: post
title: "Y'en a marre des fonctions a 2356 paramètres"
date: "2008-04-04"
categories: 
  - "web"
tags: 
  - "arguments"
  - "array"
  - "astuces"
  - "coup-de-gueule"
  - "function"
  - "http"
  - "parse_str"
  - "php"
  - "wordpress"
  - "yen-a-marre"
---

Tout bon codeur a été un jour un boulet comme tout [Espada a été un jour un Hollow](http://bleach.wikia.com/wiki/Hollow "Comment devenir un Espada lorsque l'on est un hollow"), Wouah la référence qui tue!! Je viens de tomber sur le code du premier site en PHP que j'ai codé il y a plus ou moins 10 ans. Et c'est vraiment pas beau à voir/lire. Pire, je suis incapable de comprendre qui fait quoi car il faut croire qu'à l'époque le mot documentation était tabou chez moi :) . Bref pourquoi je parle de nostalgie et de coup de gueule, c'est parce que 10 ans plus tard je retrouve dans certaines applications dites évoluées les même erreurs de jeunesse de mon code et ça me fout les boules.

Je vais prendre en exemple une fonction de mon vieux site dont j'ai honte. Attention vous allez avoir mal au yeux : \[sourcecode language="php"\]$found\_users = search\_users( $str\_region=NULL, $str\_type=NULL, $int\_ageInf=18, $int\_ageSup=100, $bool\_icon=false , $int\_start=0, $int\_viewsize=10, $str\_pseudo=NULL, $gender='mal');\[/sourcecode\] Rien qu'en lisant l'appel à cette fonction on sait ce qu'elle fait. Elle permet la recherche de personnes selon des critères spécifiques. Pourquoi ce code est pourri ? Parce que si sur le papier c'est sympa de lister tous les critères, à l'utilisation cette fonction est tous sauf intuitive. Cette fonction possède 9 arguments dans un ordre précis. Chaque argument vient avec des conditions spécifiques. Bref c'est la galère pour utiliser cette fonction en production. Vous serez toujours obliger de faire appel à votre documentation, si vous en avez une, pour connaître ne serait-ce que l'ordre des arguments de la fonction. Bref ce type de fonction est à proscrire. C'est pourquoi si je devais mettre à jour cette fonction, voici comment évoluerait l'appel à cette fonction : \[sourcecode language="php"\]$search\_params = array( 'region' => NULL , 'type' => NULL , 'age' => array( 'inf' => 18 , 'sup' => 100) , 'icon' => false, 'start' => 0 , 'viewsize' => 10, 'pseudo' => NULL, 'gender' => 'mal' ); $found\_users = search\_users ( $search\_params );\[/sourcecode\] Et oui maintenant, il n'y a plus qu'un seul paramètre et c'est un tableau ou array. Ce tableau contient n champs associatifs qui reprennent les paramètres de la première fonction. La fonction pourra évoluer et se voir ajouter ou retirer autant de paramètres que l'on veut sans porter préjudice à son utilisation à travers le site. Seul le code interne de la fonction sera modifié en fonction de c'es ajout et ou retrait de valeur. C'est la même approche que semble utiliser certaines [_template\_tags_ de Wordpress](http://codex.wordpress.org/Template_Tags/wp_list_bookmarks "Exemple d'un template_tags qui utilise cette méthode") sauf qu'au lieu de soumettre un tableau, concept peut-être trop difficile pour un designer et/ou une personne qui veut juste jouer avec son thème, on soumet _une requête HTTP_ à la fonction. Je suppose que dès lors la première action des fonctions _WordPress_ appelées de cette manière est d'utiliser la fonction [`parse_str`](http://www.php.net/manual/fr/function.parse-str.php "comment utiliser la fonction parse_str") de PHP qui transforme en tableau une requête HTTP et la fonction se retrouve alors dans les même conditions avantageuses que la nouvelle version de ma fonction CQFD ;) .

**Pour conclure, cette astuce est utilisable en dehors du PHP, ainsi, en Javascript , on substituera le tableau associatif de PHP par une variable Javascript de type objet.** Cette modification ne doit pas vous faire oublier de vérifier dans votre fonction les données qui lui sont envoyées, et là encore le faire d'envoyer un tableau associatif ou un objet rend cette tache beaucoup plus facile. Cette astuce est à réserver aux fonctions de plus de 3 arguments. Mais ça c'est mon avis personnel.
