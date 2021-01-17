---
title: "Utilisez L'Event Delegation comme une chef"
date: "2008-08-25"
categories: 
  - "web"
tags: 
  - "event-delegation"
  - "event-handler"
  - "javascript"
---

Qui ne sait pas retrouver un jour avec une liste de liens auxquels il fallait ajouter un évènement pour exécuter tel ou tel script lorsqu'on clique dessus. généralement on se retrouve alors avec une soupe HTML qu'il faudra bien maintenir sur le site et ce n'est pas la meilleur façon de coder en HTML de toute façon. Il existe une méthode simple et facile de réduire le nombre d'évènements et surtout de centraliser leur gestion, c'est la délégation d'Evènement ou en bon anglais l'Event Delegation, késako ? C'est le fait d'utiliser un élément parent commun à un ensemble d'éléments pour monitorer les évènements qui leur sont associés et activer en fonction des conditions l'une ou l'autre fonction. Si vous comprenez pas mon charabia c'est normal, un simple exemple vaut mieux que mille discours ;) . Partons du code suivant :

\[sourcecode language='javascript'\]

- **lien 1**
- [lien 2](index.html "j'aime avoir des trucs à dire")
- [lien 3](index.html)
- [lien 4](index.html "moi aussi, j'aime avoir des trucs à dire")
- [lien 5](index.html)
- [lien 6](index.html)

\[/sourcecode\]

En utilisant l'Event Delegation tel que me l'a suggéré [cette article](http://usabletype.com/weblog/event-delegation-without-javascript-library/ "Event delegation without a JavaScript library"), nous allons progressivement simplifié notre code et vous ne pourrez plus vous passez de cette technique. Suivez le guide :

1) On retire tous les évènements que l'on ne veut plus voir et on en garde 1 mais pas n'importe où :

\[sourcecode language='javascript'\]

- **lien 1**
- [lien 2](index.html "j'aime l'event delegation")
- [lien 3](index.html)
- [lien 4](index.html "moi aussi j'aime l'event delegation")
- [lien 5](index.html)
- [lien 6](index.html)

\[/sourcecode\]

Et là on utilise la magie du javascript et on obtient :

\[sourcecode language='javascript'\]
function justDoIt(event) {
    var el = getEventTarget(event);
    if (/^a$/i.test(el.tagName) && a.title != '') {
        doThat(el);
        return false;
    } else if (/^strong$/i.test(el.tagName)) {
        doThis(el);
        return false;
    }
}

function doThis(el) {
    alert(el.innerHTML);
}

function doThat(el) {
    alert(el.title);
}\[/sourcecode\]

**Explications :**

Tout d'abord, l'élement principal c'est la fonction qui va nous permettre de déterminer sur quel élément on vient de cliquer, c'est ce que je fais avec la fonction suivante :

\[sourcecode language='javascript'\]
function getEventTarget(e) {
    var o = e || window.event;
    var el = o.target || o.srcElement;
    if (el.nodeType===3) { //rajouter pour corriger un ancien bug de Safari
        el = el.parentNode;
    }
    return el;
}
\[/sourcecode\]

Ensuite on regarde si on clique bien sur l'élément qui nous intéresse, c'est-à-dire qui remplit vos conditions. Pour cela j'utilise les expressions régulières et les propriété de l'élément sélectionné pour déterminer si cet élément m'intéresse. En fonction de l'intérêt que j'ai pour l'élément, le script éxécute ou pas notre fonction.

Dernière touche, en utilisant [une fonction de gestion des Evènements Javascript](http://fn-js.info/snippets/addevent "fonction de gestion des évènements indépendantes d'un navigateur") on peut même retirer le dernier `onclick` qui subsite dans la page pour réduire au maximum la présence du javascript dans notre page. On aura donc dans un tag `script` suivant la liste ou en fin de page l'insertion javascript suivante :

\[sourcecode language="javascript"\] 

<script type="text/javascript">Events.addEvent(document.getElementById('main_menu'),'click',justDoIt);<script>
[/sourcecode]</pre>
<div></div>
Soit dit en passant c'est cette technique que j'utilise pour l'affichage de mon sous-menu lorsque l'on clique sur certaines rubriques du menu principal du thème courant de mon blog ;).</x-turndown></script>
