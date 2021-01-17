---
title: "Pure HTML post it"
date: "2011-05-25"
categories: 
  - "web"
tags: 
  - "box-shadow"
  - "css"
  - "javascript"
  - "opera"
  - "postit"
  - "transformation"
---

Here's a little trick that I've come up with yesterday after seeing what a colleague of mine was trying to achieve using background images. I've created an html Post It using css 2.1 and css3 properties. This example should work on any recent browser and degrade gracefully on older versions of IE. The only problem that I encountered was with _Opera 11.10_ [with a little CSS bug when rendering the `<tfoot>` CSS property](http://globeprgroup.com/tests/opera-bugs/opera-bug-css-tfoot.html "Opera CSS bug: wrong styling of TFOOT").

Voici une expérience CSS3 que j'ai concocté hier après avoir vu un collègue essayé de créer une effet papier autoadhésive amovible en utilisant une image d'un Post It vierge en image d'arrière plan. Ma version elle est basée à 100% sur du HTML + CSS et se décline sans problème sur les versions anciennes de Internet Explorer qui ne prennent pas en charge tous le CSS 2.1 ou les propriétés émergentes du CSS3. [Je n'ai rencontré qu'un seul bug mineur sous _Opera 11.10_](http://globeprgroup.com/tests/opera-bugs/opera-bug-css-tfoot.html "Opera CSS bug: wrong styling of TFOOT") que je n'ai pas essayé de corriger car il n'est pas lié à l'effet Post It mais plutôt au rendu des propriétés CSS appliqué à la balise  `<tfoot>` du tableau utilisé dans la page.

**Demo:** [Pure CSS PostIt](http://www.nyamsprod.com/test/postit.html "Pure CSS PostIt")
