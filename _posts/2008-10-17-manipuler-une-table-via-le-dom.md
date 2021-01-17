---
layout: post
title: "Manipuler une table via le DOM"
date: "2008-10-17"
categories: 
  - "web"
tags: 
  - "createtfoot"
  - "createthead"
  - "deletecell"
  - "deleterow"
  - "dom"
  - "insertcell"
  - "insertrow"
  - "javascript"
  - "table"
  - "tbodies"
  - "thead"
---

Lorsque l'on apprend le DOM, [la plupart des didactitiels](http://nyamsprod.com/tutorial-dom-16.html "Création d'une table via DOM Level 1") que l'on trouve sur le net se termine en montrant comment on peut créer "_from scratch_" une table en utilisant uniquement les propriétés du DOM Level 1. Du fait de la complexité de la structure d'une table en HTML, cet exemple montre l'efficacité du DOM, mais oublie de mentionner au développeur l'existence de propriétés et de méthodes DOM plus simples pour manipulation les tables HTML. [![](images/dom_table-150x150.gif "DOM Tables pour les nuls")](http://www.nyamsprod.com/blog/wp-content/uploads/2008/10/dom_table.gif)Pour utiliser ces méthodes et ces propriétés spécifiques, il faut tout d'abord pouvoir sélectionner la table que l'on veut manipuler. Pour cela, rien de plus simple que d'utiliser `getElementById` par exemple. Une fois la table sélectionnée, la manipulation de celle-ci devient un jeu d'enfant. Le DOM va représenter la table comme étant un tableau composé de lignes (`rows`) et chacune d'entre elle sera composée de cellules (`cells`). Ainsi, si je veux accéder à la troisième case de la 5ème ligne de ma table je pourrais écrire le code suivant :

\[sourcecode language="javascript"\]var mycell = document.getElementById('matable').rows\[2\].cells\[4\];
//Rappel : en javascript l'indexation des tableau commence par 0\[/sourcecode\]

Il existe une multitude de méthodes spécifiques et grâce à celles-ci et au DOM on peut plus facilement [construire une table](/test/tableau/demo.html). Petit bémol, **Il faudra se rappeler que si l'on peut accéder aux balises spécifiques des cellules, `th` et `td`, via la méthode `cells`, en revanche, on ne peut pas créer de balises `th` avec la méthode d'insertion de cellule `insertCell`.**[](/test/tableau/demo.html)

[Retirer](/test/tableau/demo.html) ou  [ajouter une ligne](/test/tableau/demo.html) est tout aussi facile. Noter que pour ajouter une ligne en fin de tableau, il suffit de donner comme index `-1` à la méthode `insertRow`. Autre remarque, l'ajout de cellules lors de la création d'une ligne n'est pas obligatoire, `insertRow` ajoutera la ligne mais celle-ci ne contiendra aucune cellule. Que peut-on retirer de ces exemples ?

1. Les lignes et les cellules sont manipulées en fonction de leur index dans le tableau qui représente notre table. Lors du changement du nombre de lignes ou de cellules, le tableau est automatiquement ré-indéxé.
2. La balise de référence à partir de laquelle la manipulation des lignes est réalisée est très importantes. En fonction de cette balise, (`table`, `thead`, `tfoot`, `tbody`) l'indexation et donc la manipulation des lignes est différentes.
3. Lorsque l'on crée une table via javascript la balise `tbody` est implicitement créée par le navigateur. Une table pouvant contenir plusieurs `tbody`, la localisation du `tbody` que vous désirez manipuler peut se faire avec la méthode DOM `getElementsByTagName`.
4. La balise de référence lors de la manipulation des cellules via leurs méthodes respectives, `insertCell` et `deleteCell` est leur ligne parent (`tr`).
5. Il existe une différence majeur entre `deleteCell`, `deleteRow` et `[removeNode](http://nyamsprod.com/tutorial-dom-15.html "La méthode RemoveNode du DOM expliquée")`. `removeNode`, à l'inverse de `deleteCell` et de `deleteRow` n'efface pas définitivement le noeud du document et permet de ré-insérer celui-ci ailleurs.

En mixant ces différentes méthodes avec le DOM et le javascript de tous les jours j'ai pu réaliser [un script qui me permet de faire bouger les différentes lignes d'un tableau](/test/tableau/index.html) très facilement. Il existe d'autres [propriétés spécifiques aux tables](http://www.javascriptkit.com/domref/tablemethods.shtml "toutes les méthodes spécifiques pour la manipulation des tables"), mais je n'ai exposé que les méthodes que j'ai estimé les plus utiles.
