---
title: "redécouvrons ensemble les joies de la table"
date: "2009-12-21"
categories: 
  - "web"
tags: 
  - "nth-child"
  - "coupe-du-monde"
  - "css3"
  - "football"
  - "rgba"
  - "table"
---

Un petit poste pas si rapide que cela sur la joie d'utilisation du CSS3 pour styler un tableau.. il n'y a que ça pour me faire passer des vacances de Noël au top ;) . Geek un jour Geek toujours que me disait un mien ami récemment. Le sempiternelle problème que je vais aborder ici est celui de styler une table de manière cool sans avoir recours à la multiplication de l'attribut `class`. Ou comme dirait un magicien .. avec rien dans la manche gauche et rien dans la manche droite.. ou presque.

Pour cela rien de plus simple... en apparence. Tout d'abord il faut un tableau quoi de plus normal, ensuite il faut un tableau avec tous pleins d'infos qu'on ne sais pas à quoi cela peut bien servir? Et si je prenais les groupes de la prochaine coupe du monde de football en Afrique du Sud. Comme je suis fainéant de nature et par conviction, je prendrais en exemple le groupe le plus nul de cette compétition... c'est-à-dire le groupe avec la France :) . Ben quoi j'ai bien le droit de placer des blagues... Un geek qui place des blagues sur le foot cela ne court pas les rues :D .

Comme je veux faire cela très rapidement et sans me casser la tête voici le résultat final en image et [en action](http://nyams.planbweb.com/test/css/).

[![](images/table-rendu-finale-300x95.png "Rendu finale grâce au CSS3")](http://www.nyamsprod.com/blog/wp-content/uploads/2009/12/table-rendu-finale.png)Vous noterez au passage que cela fonctionne sous tous les navigateurs modernes à l'exception de celui dont il ne faut pas prononcer le nom :) (il parait que c'est péché!!).

Autre remarques, plus intéressantes celle-là:

- je n'ai utilisé pour ainsi dire que 3 couleurs pour rendre l'effet du tableau. Le reste, c'est la valeur de l'_alpha_ (le fameux `a` dans `rgba` qui le fait.
- Notons au passage un apport remarqué des `:nth-child` que je l'avoue je ne maitrise pas très bien mais qui me font augurer des nuits chaleureuse en calcule mentale de ouf pour déterminer quels lignes ou quelles colonnes sera sélectionner... CSS3 power ;).
- Mention spéciale à `:hover` un pseudo attribut que si on l'avait pas inventé... on serait vraiment dans la mouise.
- le choix de la couleur de fond pour le tableau est important car c'est lui qui va conditionner la couleur résultant du `:hover` avec la valeur alpha.
- seul l'ajout des drapeaux est obligatoire via l'utilisation de l'attribut class mais si vous allez faire un site uniquement parlant de foot ou de coupe du monde... les déclarer en css vous aidera à gagner quelque lignes html dans votre code.. c'est toujours cela de ganger!!
