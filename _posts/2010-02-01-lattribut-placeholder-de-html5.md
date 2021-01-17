---
layout: post
title: "L'attribut placeholder de html5"
date: "2010-02-01"
categories: 
  - "web"
tags: 
  - "ajax"
  - "formulaire"
  - "gecko"
  - "html5"
  - "object-detection"
  - "placholder"
  - "presto"
  - "trident"
  - "webkit"
---

Comme vous le savez sans aucun doute **le** _**html5**_ **c'est le nouvel** _**Ajax**_**, mais lui,  il lave encore plus blanc que blanc :) .** Non plus sérieusement, je vais vous présenter un nouvel attribut assez intéressant et dont vous ne pourrez sans doute plus vous passer dans les années à venir: l'attribut _placeholder_. Cette attribut, tout le monde le connait et l'a déjà implanté dans l'un ou l'autre de ses sites sans même le savoir. Son utilisation qui n'est pas obligatoire et toute de même assez importante. Il sert à montrer du texte d'information dans un champs de formulaire. Ce texte, lorsqu'on clique sur le champs auquel il appartient, disparait et vous laisse remplir le champs avec le contenu que vous avez réellement envie d'envoyer. Cette technique est largement utilisée de nos jours pour montrer une information permettant le remplissage plus approprié d'un formulaire. Mais avec l'attribut _placeholder_, tout est géré par le Navigateur et non via javascript.

la bonne nouvelle, c'est que l'attribut _placeholder_ est déjà implanté dans _Webkit_ et, de fait, il fonctionne déjà dans les dernières versions de _Safari_ et de _Chrome_ (Chrome 4 si j'ai tout bien compris). la mauvaise nouvelle, c'est qu'en dehors de _Webkit_ personne ne le comprends... encore. Mais cela n'est pas grave, grâce au _javascript_ et au code qui suit ci-dessous, vous allez pouvoir remédier à ce problème de _IE6_ (beuuuh) à _FF 3.6_ en passant même par la pré-build de _Opera_ 10.5, c'est pour dire.

Je tiens à préciser que pour la rapidité de codage et parce que tout le monde l'aime bien j'ai utilisé _jQuery_ dans sa version la plus récente la 1.4.1 . Mais pour les nostalgiques et les ringards comme moi, il est tout à fait possible d'écrire ce code sans utiliser de framework. D'ailleurs cela serait un très bon exercice pour ceux d'entres vous qui se disent guru en javascript ;) .

Voici le code utilisé :

\[source lang="js"\]jQuery(function($){ //fontion de verification par object detection que le navigateur comprend ou non l'attribut placeholder var isPlaceholderSupported = function () { var o = document.createElement('input'); return 'placeholder' in o; }; //si il ne le comprends pas alors on sevit if (!isPlaceholderSupported()) { var togglePlaceholderText = function (el) { var color = '#999', v = $.trim(el.val()), p = el.attr('placeholder'); if (v == '') { el.val(p); el.css({'color':color}); } else if (v == p) { el.val(''); el.css({'color':''}); } }; $('input\[placeholder\]') .each(function(){togglePlaceholderText($(this));}) .click(function(){togglePlaceholderText($(this));}) .blur(function(){togglePlaceholderText($(this));}) .closest('form').submit(function(){$(this).find('input\[placeholder\]').each(function(){togglePlaceholderText($(this));})}); } });\[/source\]

Et parce que vous m'êtes sympathique, [la page d'exemple qui va avec](http://nyamsprod.com/test/placeholder/). _**Attention** d'autres nouveautés assez intéressantes du html5 ont étaient utilisées pour encore plus épicer le code... les découvrirez-vous ???_

Enfin, notez que mon code :

1. s'assure de ne pas soumettre la valeur de l'attribut _placeholder_ dans le cas où le formulaire et soumis avec le champs ayant pour valeur celle de son attribut _placeholder_.
2. ne fonctionne QUE dans le cas où le navigateur ne gère pas encore l'attribut _placeholder_. Wouahhh comment tu fais ? Tu détectes le navigateur alors? Non jeune padawan.. je fais de l'Object Detection ;) .

A bon entendeur/lecteur/codeur .. je vous salue!!
