---
layout: post
title: "Est-ce que ma page à la même dimension que mon document ?"
date: "2007-03-02"
categories: 
  - "web"
tags: 
  - "dom"
  - "javascript"
  - "viewport"
  - "window-dimensions"
---

Je sais cette question empoisonne la vie des humbles developpeurs de sites web que nous sommes. Alors d'emblé j'y réponds sans détour **NON!!**. Et de continuer sur ma lancée en disant que c'est tellement ennuyeux de calculer se genre de données qu'après plusieurs recherche sur le net, et plusieurs essais et erreurs, car je ne comprenais pas très bien aussi au départ, j'ai décidé de mettre dans une fonction les réponses à toutes ces questions afin que je ne me l'ai pose plus car récemment j'ai du utilisé ces données un peu trop souvent. Et les recoder à chaque fois cela devient pénible à la fin donc voici la fonction en brute, sans exemples car j'ai pas le temps en ce moment... \[sourcecode lang="javascript"\]var dimension\_detect=function(){ var d={ 'viewW':0, //viewPort Width 'viewH':0, //viewPort Height 'docH':0, //document Height 'docW':0, //document Width 'left':0, //content Left Position according to the document flow 'top':0 //content top position according to the document flow }; if(document.body.scrollHeight>document.body.offsetHeight){ d.docW=document.body.scrollWidth; d.docH=document.body.scrollHeight; } else { d.docW=document.body.offsetWidth; d.docH=document.body.offsetHeight; } if(self.innerWidth){ d.viewW=self.innerWidth; d.viewH=self.innerHeight; d.left=window.pageXOffset; d.top=window.pageYOffset; } else { var ie=(document.compatMode&&document.compatMode!='BackCompat')?document.documentElement:document.body; d.viewW=ie.clientWidth; d.viewH=ie.clientHeight; d.left=ie.scrollLeft; d.top=ie.scrollTop; } return d; };\[/sourcecode\] Bon ok je vais être sympa et je vous montre ce que cela donne pour ce billet
