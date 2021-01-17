---
title: "Google plus button generated markup"
date: "2012-03-29"
categories: 
  - "web"
tags: 
  - "1"
  - "documentation"
  - "google"
  - "html5"
  - "javascript"
  - "markup"
  - "stylesheet"
  - "tables"
---

## Bon à savoir :

Le script qui génère les boutons Google+ ajoute dans votre page, outre une `iframe` (par bouton), des balises `div`, `ins` mais surtout des balises `table` au survol du bouton :( . Souvenez-vous en le jour où l'infobulle de Google+ a un rendu bizarre mais que vous ne savait pas pourquoi. Modifier votre feuille de style au niveau des propriétés des `table` Mais pourquoi Google ne le dit pas sur [sa page de documentation](https://developers.google.com/+/plugins/+1button/ "+1 Button") ?

## Reminder:

Googleplus button script generated many tags, an `iframe`, a `div` and an `ins` tag but above all, some ugly `table` tag. So if fore some obscure reason the google plus info popup look ugly check your CSS and try to adapt the generic tables rules.

The only question is why on earth google does not share this info on [the Button+1 documentation page](https://developers.google.com/+/plugins/+1button/ "documentation") ?
