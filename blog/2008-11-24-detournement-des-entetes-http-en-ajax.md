---
title: "Détournement des entêtes HTTP en Ajax"
date: "2008-11-24"
categories: 
  - "web"
tags: 
  - "ahah"
  - "ajax"
  - "http"
  - "http-headers"
  - "javascript"
  - "json"
  - "php"
  - "xml"
---

Il existe 3 manières d'utiliser l'objet `XMLHTTPRequest` pour échanger des informations avec votre serveur. On peut utiliser le support historique qu'est le _XML_. Le problème étant qu'ensuite il faut parser le fichier _XML_ via _javascript_ avant de pouvoir en utiliser le contenu. Dire que cela est laborieux est un euphémisme, c'est tout simplement chiant à faire. C'est à cause de la complexité de ce traitement que l'utilisation de la notation _JSON_ a gagné en popularité. [Avec le](http://www.json.org/js.html "Tout sur la notation JSON") _[JSON](http://www.json.org/js.html "Tout sur la notation JSON")_ plus besoin de parser le _XML_, les données sont accessibles directement en _javascript_ via la fonction `eval` de manière natif. Dans le cas où vous ne faites pas confiance à la source de votre flux d'information, le recours à un parser _JSON_ est recommandé. Le problème de cette approche et que si vous ne désirez modifier qu'un élément de votre page contenant plus ou moins beaucoup d'informations, il vous faudra exceller en DOM pour mettre à jour l'affichage de votre page. C'est dans ce dernier cas que la 3ème et dernière technique l'AHAH (Asynchrone Html And HTTP) est approprié. Très simple d'utilisation, [l'](http://ajax.phpmagazine.net/2005/11/ahah_asychronous_html_and_http.html "Explication du fonctionnement de l'Asynchrone HTML and HTTP")_[AHAH](http://ajax.phpmagazine.net/2005/11/ahah_asychronous_html_and_http.html "Explication du fonctionnement de l'Asynchrone HTML and HTTP")_ [combine l'objet l'](http://ajax.phpmagazine.net/2005/11/ahah_asychronous_html_and_http.html "Explication du fonctionnement de l'Asynchrone HTML and HTTP")`[XMLHTTPRequest](http://ajax.phpmagazine.net/2005/11/ahah_asychronous_html_and_http.html "Explication du fonctionnement de l'Asynchrone HTML and HTTP")` [et la méthode](http://ajax.phpmagazine.net/2005/11/ahah_asychronous_html_and_http.html "Explication du fonctionnement de l'Asynchrone HTML and HTTP") `[innerHTML](http://ajax.phpmagazine.net/2005/11/ahah_asychronous_html_and_http.html "Explication du fonctionnement de l'Asynchrone HTML and HTTP")`. La modification d'une partie et/ou de l'entièreté de votre page se fait dès lors quasi instantanément. En résumé :

1. Vous construisez côté serveur la partie _HTML_ que vous désirez ajouter à votre page;
2. Vous la récupérez via `XMLHTTPRequest` dans votre page;
3. Vous l'incluez dans l'élément de votre choix via `innerHTML`

...et hop c'est dans la boîte. Et voici un exemple pour illustrer mon propos :

Exemple simplifié d'une page PHP côté serveur appelé via `XMLHTTPRequest`

\[sourcecode language='php'\]

**This is changed via Ajax**

'; echo $ajax; ?>\[/sourcecode\]

Côté client on récupère via l'objet `XMLHTTPRequest` le contenu du fichier PHP en l'occurence $ajax.

\[sourcecode language='javascript'\]//soit XHR l'objet XMLHTTPRequest if (XHR.readyState === 4) { if (XHR.status === 200) {  // On a recu une reponse correcte du serveur document.getElementById('content').innerHTML = XHR.responseText // XHR.responseText correspond à la valeur de la variable PHP $ajax; } }\[/sourcecode\]

Le problème avec l'_AHAH_ c'est qu'on ne peut modifie qu'un élément de la page par requête. Que se passe-t-il si l'on veut modifier 2 ou 3 éléments indépendants du site via une une requête HTTP ? Une solution, pour contourner le problème serait de modifier l'entièreté de la page... Mais cela réduit à néant l'avantage de  l'utilisation de l'_Ajax_. En fait, ce serait bien de combiner la simplicité du _AHAH_ avec une certaine flexibilité que l'on retrouve avec l'utilisation du _JSON_ ou du _XML_, alors comment faire ?

En regardant de plus près l'objet `XMLHTTPRequest` on se rend compte que celui-ci possède 2 méthodes méconnues :

- `setResponseHeader`, capable de créer et d'envoyer des entêtes HTTP;
- `getResponseHeader`, capable de recevoir et de lire les entêtes HTTP.

D'où l'idée totalement immonde de [détourner les entêtes HTTP](http://www.php-experts.org/developpement-web/php-developpement-web/erreur-404-redirection-301-headers-et-codes-de-reponse-http-courants-24 "Ce à quoi peuvent servir réellement les entêtes HTTP") pour envoyer des informations supplémentaires qui me permettraient de changer d'autres aspects de ma page tout en gardant la facilité d'utilisation de la méthode `AHAH`.

Je sais les puristes me diront que les entêtes HTTP ne servent pas à ça, certains m'ont même dit :

> le respect des RFC en matières de proxy HTTP, c'est un peu comme le respect des standards du XHTML strict par les développeurs web.

Sachant que ma technique est un peu barbare, je me suis restreins dans l'utilisation de celle-ci. C'est déjà assez mal de le faire alors je ne l'utilise que pour envoyer vers mon client des informations minimales de type :

- pseudo booleéns (ex: 't/f' ou 'KO/OK');
- des nombres;

Mais rien n'empêcherait un esprit mal intentionné d'envoyer encore plus d'informations via cette méthode... bien que je ne le recommande pas. Encore une fois je le dis, [les requêtes HTTP ça sert pas à ça](http://www.w3.org/Protocols/rfc2616/rfc2616.html "La RFC qui définie le rôle des RFC").  Avec mes requêtes HTTP "fait maison" j'envoie donc des données pouvant entrainer des changements locaux contrôler par javascript en suivant la méthode suivante :

Côté serveur, on aura :

\[sourcecode language='php'\]

**This is changed via Ajax**

'; // $condition est la résultante de ce que le serveur a recu comme requete via Ajax $http\_header = ($condition === true) ? 'OK' : 'KO'; header('x-sajax-condition :' . $http\_header, true); echo $ajax; ?>\[/sourcecode\]

et au niveau de mon javascript je récupère l'information très simplement

\[sourcecode language='javascript'\]//soit HR l'objet XMLHTTPRequest if (XHR.readyState === 4) { if ( HR.status === 200) {  // On a recu une reponse correcte du serveur var cond = HR.getResponseHeader('x-sajax-condition'); if (/OK/.test(cond)) { //changement si la condition est OK } else { //changement si la condition est KO } document.getElementById('content').innerHTML = HR.responseText; } }\[/sourcecode\]

Et voila, que pensez-vous de cela... C'est mal, je sais, pensez-vous qu'il existe une autre manière pour obtenir la même fléxibilité tout en utilisant l'_AHAH_ ? Si oui, je suis preneur ;) .
