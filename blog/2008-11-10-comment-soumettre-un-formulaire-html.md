---
title: "Comment soumettre un formulaire HTML"
date: "2008-11-10"
categories: 
  - "web"
tags: 
  - "button"
  - "didactiel"
  - "form"
  - "formulaire"
  - "html"
  - "image"
  - "input"
  - "soumission"
  - "tutorial"
  - "typeimage"
---

La soumission de formulaire est l'activité la plus importante sur internet. L'inscription à un site de rencontre, les transactions bancaires pour acheter son ticket d'avion ou l'ajout de commentaires sur un blog, toutes ces actions se font via la soumission d'un formulaire. Les développeurs web sont donc devenu, à la longue, des spécialistes de la validation de formulaire, via Javascript, côté client, via les langages scripts, côté serveur. Nous passons tellement de temps à valider nos formulaires que l'action même de les envoyer du client vers le serveur est passée au second plan. J'en profite donc pour rappeler, exposer ou faire découvrir à certains, les différentes manières de soumettre un formulaire via HTML.

Suivant les recommendations du W3C :

- Si votre bouton de soumission ne contient pas d'attribut `name`, le formulaire sera envoyé mais l'information de la balise de validation ne sera pas prise en compte. 
- Seule la valeur de l'attribut `value` de la balise de soumission est prise en compte lors de l'envoie d'un formulaire.
- Lorsqu'un formulaire contient plusieurs boutons de soumission, **seule** la valeur de l'attribut `value` de la balise que l'on aura cliqué sera envoyée, les autres balises de soumissions ne seront pas prise en compte.

Sachant cela, et aussi surprenant que cela puisse paraître à certain, **Il existe 2 balises et 3 manières de soumettre un formulaire HTML**. Et bien que complémentaires, chacune de ses techniques possède des avantages et des inconvénients. 

## En utilisant la balise INPUT avec l'attribut type=submit

\[sourcecode language="javascript"\]\[/sourcecode\]

C'est de loin la technique la plus utilisée. Son utilisation est tellement simple et intuitive que la majorité des développeurs n'utilisent **que** cette technique, par paresse, par manque de temps.. ou, tout simplement, parce qu'ils n'ont pas encore lu mon article ;) . L'avantage de cette technique et qu'elle fonctionne sous tous les navigateurs. Elle est simple à implanter, ne contient aucun bug et aucune surprise ne nous attend. Les désavantages de cette balise sont pourtant légions :

- Le contenu texte de la balise reflète directement la valeur de l'attribut **value**, donc on ne peut pas écrire ce que l'on veut
- Seule l'utilisation de CSS permet de rendre le bouton plus attrayant

## En utilisant la balise INPUT avec l'atribut type=image 

\[sourcecode language="javascript"\]\[/sourcecode\]

A l'époque ou le CSS n'existait pas encore, cette technique était très répandue. En indiquant le `type="image"`, votre navigateur s'attend à trouver 2 attributs en plus dans la balise `input`, les attributs `src` et `alt` comme ceux utilisés dans la balise `img`. Vous avez compris, le formulaire va être soumis via l'utilisation d'une image comme bouton d'envoi. A l'époque cela avait beaucoup d'avantage on pouvait facilement rendre attrayant son formulaire. De plus, outre la valeur de l'attribut `value`, si elle existe, les valeurs des coordonées X et Y du clic de la souris par rapport à l'image sont également envoyées lors de la soumission du formulaire. Cette technique présente un désavantage non négligeable, en fonction de la compréhension du W3C par les [différents](http://www.nyamsprod.com/blog/wp-content/uploads/2008/11/image-trident-opera.png "Bug d'affichage sous Internet Explorer et Opera - Il manque la valeur de l'attribut value") [navigateurs](http://www.nyamsprod.com/blog/wp-content/uploads/2008/11/image-webkit-gecko.png "Gecko et Webkit envoient la valeur de l'attribut value"), [l'ajout ou non de la valeur de l'attribut](http://nyams.planbweb.com/test/submit/image.php "mauvaise interprétation de l'input type=image par certains navigateurs") `[value](http://nyams.planbweb.com/test/submit/image.php "mauvaise interprétation de l'input type=image par certains navigateurs")` [varie selon le navigateur](http://nyams.planbweb.com/test/submit/image.php "mauvaise interprétation de l'input type=image par certains navigateurs"). En résumé, les résultats que vous obtiendrait ne seront pas fiable. De plus avec l'adoption du CSS cette technique semble être de moins en moins utilisée. 

## En utilisant la balise BUTTON avec l'attribut type=submit

\[sourcecode language="javascript"\] ici je peux raconter ma vie et autre chose \[/sourcecode\]

De prime abord, visuellement, pour une personne qui ne fait pas attention, l'utilisation de la balise button associée à l'attribut `type="submit"` est identique à l'utilisation de la balise input, mais il n'en est rien. La grande différence est que l'on peut rajouter autant de texte et de contenu que l'on veut avec la balise button. La balise bouton n'affiche pas la valeur de l'attribut `value` mais plutôt le contenu inclut entre ses balises d'ouverture et de fermeture. cette balise offre donc une liberté maximale, et devrait être la balise préférée des designers et des développeurs, car avec ou sans CSS les possibilités de mise en valeur sont beaucoup plus importantes qu'avec la balise `input`.

Hélas, l'adoption de cette balise sur un site de production n'est pas possible. Pourquoi ? [Parce que Internet Explorer jusqu'à sa version 8 l'implante mal](http://nyams.planbweb.com/test/submit/button.php "Bug de l'implantation de la balise button sous Internet Explorer"). Au lieu de soumettre la valeur de l'attribut `value`, comme indiqué par le W3C, [IE soumet le contenu compris entre les balises d'ouverture et de fermeture de la balise button](http://www.nyamsprod.com/blog/wp-content/uploads/2008/11/button-trident.png "le contenu equivalent a innerHTML est envoyé vers le serveur"). En clair, la valeur attendu n'est pas celle que l'on reçoit. Ce bug limite donc très fortement l'utilisation de cette technique sur un site grand publique, du fait des parts de marché de IE :( .

Il serait intéressant de voir si avec la sortie de IE8 l'utilisation de la balise BUTTON va enfin augmenter, de toute les manières moi je suis pour, c'est pourquoi je l'utilise sur mon site ;) .
