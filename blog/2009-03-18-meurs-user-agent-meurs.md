---
title: "Meurs user agent, meurs!!!"
date: "2009-03-18"
categories: 
  - "web"
tags: 
  - "ajax"
  - "chrome"
  - "firefox"
  - "gmail"
  - "internet-explorer"
  - "javascript"
  - "live-hotmail"
  - "opera"
  - "safari"
  - "user-agent"
  - "user-agent-switcher"
  - "web-2"
  - "yahoo-mail"
---

Il y a quelques temps, à la sortie de _Chrome_, [je m'insurgeais contre les **user agents**](http://nyams.planbweb.com/blog/2008/09/18/yen-a-marre-des-user-agent/ "y'en a marre des user agents") et surtout les développeurs qui ce sont rués comme des mouches sur un tas de merde, sur cette chaîne de caractère immonde et inutile pour déterminer comment différencier Chrome de Safari. Et bien j'en remets une couche cette fois-ci et ma vindicte se focalise cette fois-ci contre les seniors développeurs ou ceux qu'on appellent les Gurus du Javascript... mais le sont-ils vraiment ?

Il existe dans ce bas monde qu'est l'internet des applications qui ont le don de m'agacer au plus haut point. Toutes ces applications dites Web 2 voire Web 3. C'est applications, dont certaines sont utilisées par la majorité des web surfeurs, tout les jours, ont été atteintes de la maladie de l'**Ajaxite aiguë**, dont le principal symptôme est qu'elles reposent sur l'utilisation abusive de la  méthode `XMLHTTPRequest`. [Cette utilisation intensive](http://nyams.planbweb.com/blog/2008/11/24/detournement-des-entetes-http-en-ajax/ "Détournement des entêtes HTTP") a conduits les gurus derrière ce type d'application à recourir à toutes sortes de techniques obscures et à de la technologies vaudoux comme l'utilisation de tableaux de statistiques pour déterminer sur quel navigateur et sur quel OS la version full Ajax peut-être utilisée ou pas. Qu'on se le disent, ces sites n'ont pas été codés par vous ou moi, non , ils ont été codés par des êtres à l'intelligence supérieure venu d'une lointaine galaxie et repartis depuis. Sans aucune modestie et/ou sarcasme, je l'avoue même avec une avance de 10 années **je n'aurais jamais pu coder seul ne serait-ce que le 1/4 du 1/10 d'une de ces applications**. Mais au delà de ses louanges méritées, il y a quand même un truc qui m'exaspère c'est que ces sites, censée être la vitrine de ce que le Javascript à de mieux à offrir en termes d'expériences internet ne respecte pas le _B-A-ba_ du coding.

Récemment pour un projet que je devais développer j'ai du installer un plugin fort intéressant que je recommande à tous développeur, bon ou mauvais, [User Agent Switcher](https://addons.mozilla.org/en-US/firefox/addon/59 "L'extension User Agent Switcher de Firefox"). Cette extension à Firefox permet de jongler entre  les user agents les plus courants, voire de générer un user agent spécifique. Vous me direr à quoi cela sert-il ? Et bien cela sert à faire comprendre à n'importe quel développeur que la majorité des sites du Web 2 se moquent du monde. Il m'a suffit de changer le user agent à  de mon Firefox pour qu'il devienne inutilisable sur la majorité des sites Web 2.0 dont Gmail/Google docs , Facebook et j'en passe!!  Mais ce n'est pas possible, me direz vous, et pourtant c'est vrai!! Je trouve inadmissible de se voir interdit l'entrée d'un site parce que mon user agent contient le mot **Tirefox** en lieu est place de **Firefox**. C'est stupide mais ainsi va la vie dans le monde des développeurs. Que le code d'un site amateur mal référencé et inconnu de la majorité bug ou plante à cause d'un user agent mal placé, je peux le concevoir, mais que des sites dit mainstream plante lamentablement à cause de cela.. c'est inacceptable!!! Et le pire c'est le message que l'application vous envoie... Votre navigateur n'est pas supporté, veuillez télécharger un navigateur récent compatible comme Firefox :( ... A méditer
