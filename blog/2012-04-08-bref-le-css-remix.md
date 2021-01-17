---
title: "Bref, le CSS remix"
date: "2012-04-08"
categories: 
  - "web"
tags: 
  - "animations"
  - "bref"
  - "css3"
  - "html5"
---

Une petite animation via CSS3 amusante que j'ai réalisé en moins de 2 heures et que je publie dans mon bac à sable . Le plus fun ne se trouve bien sur pas dans le fichier HTML, mais plutôt dans le fichier CSS qui gère toute l'animation. Pour la petite histoire, les 2 script JavaScripts incluents n'affectent pas directement l'animation mais facilitent son déploiement.

j'utilise :

- l'excellent script [prefixfree](http://leaverou.github.com/prefixfree/ "Break free from CSS prefix hell!") de Lea Verou pour ne pas avoir à écrire tous les versions préfixées des propriétés CSS non-stable;
- une version "custom" de [modernizr](http://modernizr.com/download/ "Modernizr is an open-source JavaScript library that helps you build the next generation of HTML5 and CSS3-powered websites.") qui détecte le support des animations CSS du navigateur afin de contourner un bug dans l'implantation sous Firefox.

Bref, c'est par ici pour [voir la démo finale](http://www.nyamsprod.com/test/bref/ "Un démo réalisée uniquement avec du CSS3").
