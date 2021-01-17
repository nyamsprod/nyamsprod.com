---
title: "Navigateurs, image au format jpeg au profil CMYK ou RGB ?"
date: "2010-03-15"
categories: 
  - "web"
tags: 
  - "cmyk"
  - "compatibilite"
  - "image"
  - "jpeg"
  - "rgb"
---

On en apprend tout les jours. Aujourd'hui je suis tombé sur un problème assez sympa. Une image qui s'affiche parfaitement sous Firefox mais qui disparait complètement sous Internet Explorer, quelque soit la version. Du coup, naïf que je suis je me suis dit que cela devait venir des entêtes de l'image mais cela n'était pas le cas. Alors ne sachant que faire j'en parle autour de moi et finalement un collègue m'apprend que cela est surement du au [codage CMYK de mon image.](http://www.commentcamarche.net/contents/video/cmy-cmj-cmyk-cmjn.php3) Et là je me dis hein ? non.. pas possible. Comme un exemple vaut mieux que 10000 mots voici une petite expérience.

D'abord l'image JPEG "classique" en RGB que tout bon navigateur pourra afficher.

[![](images/cool_aliens_vector.jpg "image JPEG au profil RGB")](http://www.nyamsprod.com/blog/wp-content/uploads/2010/03/cool_aliens_vector.jpg "image JPEG au profil RGB")

Et l'image équivalente en "CMYK". _(si vous êtes sous Internet Explorer et que vous ne voyez rien ... c'est normal!!)_

[![](images/cmyk_aliens.jpg "image JPEG au profil CMYK")](http://www.nyamsprod.com/blog/wp-content/uploads/2010/03/cmyk_aliens.jpg "image JPEG au profil CMYK")Notez que sous Firefox/Opera et Chrome (Webkit) vous ne verrez pas de différence. Là où cela devient intéressant c'est lorsque l'on utilise Internet Explorer ou Safari (Webkit).

Sous Internet Explorer. L'image n'est tout simplement pas montrée. Internet Explorer n'arrive tout simplement pas à interpréter l'image. Pour Safari, c'est plus ambigu. Bien qu'ayant un moteur similaire à celui de Chrome (Webkit pour ne pas le nommé), Safari sous Windows interprète de manière approximative l'image en CMYK du coup l'image que vous obtenez n'est pas toujours identique à celle que vous avez téléchargée ou à celle que vous avez sous Firefox. Il vous suffira pour vous convaincre de comparer les 2 images présentées ci-dessus.

**Comment remédier à ce problème ?** Pour l'instant, il n'ya pas de solution miracle à coup de javascript ou que sais-je encore. [La seule manière de résoudre le problème est de convertir en RGB](http://webdesigners-blog.blogspot.com/2009/02/internet-explorer-jpeg-cmyk-issues.html) toutes les images JPEG au codage CMYK que vous désirez afficher sur le net à l'aide de votre programme d'édition d'image préféré, en attendant que tous les moteurs de rendu arrivent à comprendre les fichiers JPEG au codage CMYK. Une petite recherche sur le net m'apprends que [ce bug date d'au moins 2006](http://www.mattcutts.com/blog/jpeg-problems-in-firefox-and-ie/) mais qu'entre temps Firefox l'a réglé... mais visiblement pas Internet Explorer et/ou Safari.

**_PS: encore un exemple qui illustre bien que Safari et Chrome bien qu'ayant le même moteur de rendu ne sont pas identique et qu'il faut hélas tester votre site dans les 2 navigateurs contrairement au dires de l'équipe de Chrome._**
