---
title: "World War IE"
date: "2010-09-20"
categories: 
  - "web"
tags: 
  - "beautyoftheweb"
  - "chakra"
  - "firefox"
  - "ie"
  - "opera"
  - "safari"
  - "trident"
  - "webkit"
---

Pour les plus perspicaces d'entre vous vous aurez compris que je vais vous parler de mes impressions après la sortie de IE9 beta 1. Pour mes lecteurs les plus assidus qui gardent encore un oeil sur mon blog, ils le savent, je détestent les béta, mais vu qu'à moins d'une catastrophe atomique on peut déjà dire que IE9 est complet à quelques bug près ça et là je vous livre mon sentiment.

Comme j'aime à le clamer **IE7 c'était IE6.5 et ce que l'on attendait dans IE7 on l'a eu.... partiellement dans IE8.** Clairement avec  les avancés des autres navigateurs la IE team se devait de produire un navigateur digne de ce nom ou mettre la clé sous la porte. Il faut croire qu'ils ont compris et c'est donc [un navigateur web du 21ème siècle que nous apporte aujourd'hui la IE Team](http://www.beautyoftheweb.com/).

### Il était temps

De but en blanc soyons honnête, IE9 est un bon navigateur, certains lui reproche le fait qu'il n'intègre pas assez de techno à la pointe comme les transitions et/ou les animations CSS ou encore la géolocation mais vu là d'où vient le navigateur on peut dire sans trop se tromper que le boulot effectué derrière pour ramener au goût du jour IE est énorme.

### Pas de IE9 pour Windows XP

Voilà le genre de commentaires que l'on sort pour essayer de réduire le boulot de la IE team, on attaque plus le produit, vu que le produit est bien pensé, non on attaque la forme, la plateforme... bref tout sauf le produit. Windows XP est sortie il y a près de 10 ans. En informatique cela représente un siècle. Je sais que comparaison n'est pas raison mais on ne demandera jamais à un constructeur d'automobile de continuer à supporter ses technologies d'avant la dernières guerre mondiale... alors pourquoi Microsoft devrait le faire ?

### Un navigateur dans la norme

En gros c'est la sensation qui ressort après l'utilisation de ce navigateur durant ce Week-end, loin de ré-inventer la roue, IE9 en fait essaie de piquer ça et là le meilleur des autres navigateurs et le propose à sa manière avec plus ou moins du succès. L'œil aguerrit du développeur que je suis reconnaitra les emprunt fait à _Chrome, Firefox, Opera_ ou encore _Safari_. Qu'à cela tienne, je ne vais pas le leur reprocher car en leur temps chacun de ses navigateurs ont fait **et** continu de le faire vis-à-vis de leurs concurrents. Tout le monde copie tout le monde avec le secret espoir d'être celui qui arrivera à mieux présenter un concept créé et/ou tester par l'autre. Alors, oui IE9 ressemblent farouchement à Chrome/Safari et alors ?

### Les points qui fâchent... parce qu'il y en a ;)

_(si vous n'êtes pas développeur ou curieux... passez votre chemin ... franchement si vous êtes un adepte de Internet Explorer... télécharger IE9 ... vous serez surpris de voir le web... différemment = comme 50% du reste du monde quoi ;) )_

**1°) la fameuse accélération matérielle.**

Une leçon apprise par Microsoft durant le développement de IE9. Entre l'annonce, l'implantation stable et la sortie d'un produit final, la IE team devrait apprendre à accélérer (jeu de mot no-intentionnel) leur mouvement sinon leurs innovations n'en sont plus au moment de leur sortie réelle. Firefox a déjà implanté l'accélération matérielle et si cela continue Mozilla aura un produit stable et sortie **AVANT** Microsoft, le premier à annoncer l'accélération matérielle.

**2°) Microsoft, arrêtez de comparer des pommes avec des poires :( .**

Oui, cela devient véritablement énervant. En vous rendant sur [leur superbe site de comparaison on verra 2 tableaux](http://windows.microsoft.com/en-US/internet-explorer/products/ie-9/compare?T1=tab2). Un tableau qui compare IE9 avec différents navigateurs. Ce sur quoi je ne reviendrait pas c'est la comparaison entre IE9 et les anciennes versions de IE. Sérieusement, si il y avait une régression, IE9 ne serait pas sortie, donc tout le monde s'en fout :) . Non là où cela m'énerve c'est lorsqu'on se met à comparer _IE9 beta 1_ avec d'autres _beta_. Je trouve cet exercice totalement ridicule, pour ne pas dire autre chose. C'est comme si on comparait 2 prototypes de voiture non encore sorties. Certes on a affaire à 2 voitures qui vous mènent d'un point A à un point B mais vu qu'elles ne sont pas encore sorties.... toutes les deux, le tableau en question n'apporte aucune information pertinente car les 2 modèles sont

1. sujet à changements d'ici leur sortie officielle.
2. encore en plein développement. Si je regarde les modifications entre les différentes beta de _Firefox4_ on comprend rapidement que ce comparatif est totalement obsolète : et ne parlons même pas de Chrome et de son développement encore plus original par rapport à IE9.

Le plus absurde est pourtant ailleurs, de fait IE9 n'a pas besoin de ce comparatif pour montrer ce dont il est capable. Monsieur lambda n'installera jamais 4 navigateurs pour vérifier les dires (vrai ou faux du dit tableau) et le développeur que je suis est suffisamment intelligent pour connaitre, voir et tester les faiblesses et les points forts de chaque navigateur. En clair, ce n'est pas et cela ne sera jamais une bonne idée. Si comparaison il doit y avoir que l'on compare IE9 stable avec FF 4 stable et les versions correspondantes stable de Safari, Opera et Chrome... et bonne chance pour bien les déterminer :) .

**3) Le Mode Compatible de IE9**

**[![](images/compatibility-500x106.png "compatibility")](http://www.nyamsprod.com/blog/wp-content/uploads/2010/09/compatibility.png)**Mais là où le bas blesse c'est leur "histoire" de  mode compatible. Déjà qu'avec IE8 cela m'énervait à un point vous ne pouvez pas l'imaginer... maintenant avec IE9 c'est la totale.. vous ne me croyez pas imaginer le scénario suivant.

Bon codeur que vous êtes vous codez votre site pour tous les navigateurs récents. Je rappelle que jusqu'à la semaine dernière cela signifier IE8 inclut. Comme vous codez en pensant au navigateur du futur qui supporteront tous le CSS3 sans les préfixes, vous utilisez les déclarations définitives des bords arrondis. Comme vous utilisez des images en png vous savez que votre site fonctionnera très bien sous IE8 mais qu'il éprouvera quelque problème pour tout navigateur IE inférieur. Alors comme vous êtes un codeur qui suit les recommandations des fabricants de navigateurs, vous rajouter la méta spécial de IE qui permet de déclencher la compatibilité IE8 pour que ce navigateur affiche correctement les images _png_.

<meta http-equiv="X-UA-Compatible" content="ie=8">

IE9 sort et vous apprenez avec joie que ce navigateur supporte les bords arrondis tel que définies par le W3C. Vous êtes content et vous vous rendez sur votre site pour admirer le résultat et là patatra... aucun bord arrondis à l'horizon et pourtant Opera et Webkit qui supportent également les bords arrondis eux les montrent. Vous regarder la source de votre document pour voir ce que vous avez mal codé et là l'horreur saute à vos yeux ... **en déclenchant la compatibilité pour IE8 vous avez automatiquement désactiver la compatibilité pour IE9** .. c'est con, stupide et totalement crétin... mais c'est un avantage selon le marketing de IE9 :( . Votre code est bon mais la balise meta de IE censée vous aidez vient de vous faire un coup bas.. Alors qu'elle est la solution ???

Elle est très simple, vu que je ne peux pas virer leur méta au risque de voir mon site dans un état pré-IE8 même sous IE8 , **je recommande quelque chose que la IETeam ne veut pas... et bien c'est leur faute... tous ça parce qu'il ne veulent pas casser le web :( .** A partir d'aujourd'hui sur tout site que je code je rajoute le header suivant :

<meta http-equiv="X-UA-Compatible" content="ie=edge">

Comme ça quand IE10 sortira, le problème ne se posera plus! Pénible et totalement inutile :(
