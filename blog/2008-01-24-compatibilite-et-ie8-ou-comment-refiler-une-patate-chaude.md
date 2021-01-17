---
title: "compatibilité et IE8 ou comment refiler une patate chaude"
date: "2008-01-24"
categories: 
  - "web"
tags: 
  - "browsers-war"
  - "ieteam"
  - "internet-explorer-8"
  - "navigateurs"
  - "trident"
  - "w3c"
  - "wasp"
---

Si vous n'avez pas encore lu l'article sur [Alistapart](http://alistapart.com/articles/beyonddoctype "Beyond DOCTYPE: Web Standards, Forward Compatibility, and IE8") qui a enclenché le buzz ou encore l'article sur le blog de l'IETeam qui officialise [les différents modes de rendu dans IE8](http://blogs.msdn.com/ie/archive/2008/01/21/compatibility-and-ie8.aspx "Compatibility and IE8"), c'est maintenant ou jamais. Après une telle lecture ma première réaction a été _"Fuck that!!"_ et ensuite _"Damn!!"_ et enfin _"What the heck anyway!!"_.

Maintenant avec le recul est après avoir lu et relu ces articles mais également les différentes opinions des principaux acteurs dans le blogosphère des webdeveloppeurs anglophones, j'ajoute ma contribution à la discussion en apportant ma compréhension de la décision de Microsoft et de ses implications pour nous, les Webdeveloppeurs.

### La décision en résumé

\[sourcecode language="html"\]\[/sourcecode\] Microsoft avec Internet Explorer 8 introduit un nouveau déclencheur de comptatibilité dans son navigateur, si on rajoute le code repris ci-dessus dans la partie head de votre page HTML, le plus proche du début du document vous serez dans le mode IE8 standard, _mode qui répondrai_ aux normes les plus récentes du W3C au niveau HTML et CSS. C'est sous ce mode que le navigateur a passé le [test Acid2](http://www.webstandards.org/action/acid2 "The Acid2 Test from WASP").

De plus à partir de IE8 et ces successeurs, si ce code n'apparait pas, le navigateur traitera votre document comme si il était rendu par IE7 dans son mode standard. Enfin, et pour terminer, si vous avez en plus omis d'ajouter le `DOCTYPE` dans votre document HTML, il sera rendu en Quircksmode.

Il est a noté que pour mettre à jour vos pages si vous êtes chez un hébergeur qui vous le permet, il ne vous suffira que de rajouter une commande `header` au niveau de votre serveur et tous vos fichiers seront automatiquement mis à jour, d'où la simplicité d'utilisation de ce déclencheur.

### Les implications de la décision pour IE8+

La IETeam s'occupe enfin des problèmes du moteur de rendu Trident et propose [un contrat clair](http://www.quirksmode.org/blog/archives/2008/01/the_versioning.html "The versioning switch is not a browser detect") et un comportement prévisible pour le webdeveloppeur. Voici résumé le message de Microsoft, _"Si vous suivez notre contrat tout ira bien, mais si vous ne le suivait pas, c'est votre problème, plus le notre"_. Bref Microsoft [refile astucieusement la patate chaude](http://hosanna.over-blog.com/article-7243861.html "Patate chaude et café corsé !") à nous, les web developpeurs en y ajoutant la caution morale d'une partie de la WASP pour dire voila même eux ils sont d'accord, même si [cela n'est pas totalement vrai](http://www.webstandards.org/2008/01/22/microsofts-version-targeting-proposal/ "Microsoft’s Version Targeting Proposal").

Ce qui m'interpelle dans la décision de la IETeam c'est moins l'utilisation d'un déclencheur, ce qui était prévisible, que le changement de philosophie qu'il oblige chez le Webdeveloppeur. Aujourd'hui tout **bon** webdeveloppeur code pour la meilleure des spécifications, en pensant au mieux de ses capacités, aux navigateurs les plus anciens. Jusqu'à aujourd'hui il était de la responsabilité des constructeurs de navigateurs de veiller à ce que le navigateur réponde aux exigences des spécifications. Avec ce déclencheur, c'est l'inverse que préconise la IETeam, à charge des webdeveloppeurs de mettre à jour leur code en fonction du navigateur qui lui ne changera _(plus?)_ de comportement entre version. Le risque étant que certains webdeveloppeurs cédent tôt ou tard à l'appel des codes fonctionnant uniquement pour un navigateur bien défini, et que l'on retombe dans un scénario où les bannières _best view with IEx_ renaissent de leur cendre. **In fine, c'est l'indépendance du code par rapport au navigateur qui est totalement remis en question.**

### Cassons le Web

L'argument moteur de la décision de Microsoft c'est la philosophie du _"Don't break the web"_. [Chris Wilson](http://blogs.msdn.com/cwilso/archive/2008/01/22/i-feel-happy-too.aspx "Le blog personnel de Chris Wilson qui travaille pour la IETeam") ne veut pas que du jour au lendemain un site soit visuellement rendu de manière différent entre 2 versions consécutives d'Internet Explorer. Pour ma part je défends l'argument contraire _"Let's break the Web"_. et ce pour diverses raisons :

1. Cela a déjà était fait plusieurs fois dans le passé, par exemple, entre les versions Netscape 4 et 6. Le passage vers Gecko [s'est fait dans la douleur](http://www.stopbadtherapy.com/standards.shtml "Transitioning from Proprietary DOMs and Markup to W3C Standards: Enhancing Pages That Use LAYER, document.layers[], and document.all to Support Standards") mais il a eu lieu. Et il fut salutaire car il a permis l'émergence de Firefox. Lorsqu'un moteur de rendu et/ou un navigateur est arrivé en fin de vie il faut savoir l'enterrer, AOL a sut le faire pour Netscape, Microsoft a, visiblement du mal à le faire.
2. D'autre part, l'argument _"Don't break the web"_ est toujours joint à celui beaucoup plus compréhensible de ne pas pertuber les applications vitales développées pour l'Intranet des entreprises et qui _visiblement_ dépendent de IE dans un mode que le nouveau standard d'IE8 va "_casser_". Et bien, dans ce cas, inversons le procédé préconisé par Redmond. Si vous ne faites rien vous êtes en mode standard, mais si on rajoute le déclencheur on se retrouve dans un mode Quircksmode. Si ces applications en intranet sont si vitales que cela, l'administrateur système de ses entreprises trouvera bien 5 minutes pour implanter le patch au niveau serveur et le tour sera joué. Il sera simplement du rôle des utilisateurs et de l'administrateur réseau de se tenir au courant. Et voila comment à mon tour je refile la patate chaude, que nous a refilé IE, des Webdeveloppeurs vers l'administrateur réseau, qui n'a rien demandé, voire à l'utilisateur.

In fine, tout ceci est du à l'absence de renouvellement du moteur Trident d'IE pendant 6 ans. Et à un manque de prise de responsabilité au niveau de Microsoft qui essaie de sortir la tête haute d'une situation que la compagnie a elle-même créée. La stagnation c'est l'anti-thèse du web. Le Web a toujours été un terrain en plein mouvement, essayer de mettre en place un système de versionning a une page web en fonction d'un navigateur c'est ouvrir [la boite de pandore](http://www.linternaute.com/expression/langue-francaise/80/la-boite-de-pandore/ "Origine de l'expression : la boîte de pandore") à une panoplie d'autre versioning. Est-ce que demain ce versioning se retrouvera également pour le contenu interactif ( Flash, Silverlight, Audio, Video etc...), [les langages de script](http://ejohn.org/blog/meta-madness/ "Les implications du déclencheur sur le javascript"), le HTML5 ?

Au moins une chose positive, on a plus parlé ces derniers jours de IE8 que de tout autre navigateur sur les blogs, si c'est pas de la pub gratuite alors qu'est-ce que c'est ? On en oublierait presque que Mozilla Firefox 3 et Opera 9.5 qui sont déjà en Beta.

### Ce qu'il faut retenir

1. [La "Browsers War II"](http://nyams.planbweb.com/blog/2008/01/08/browser-wars-ii-the-empire-strikes-back/ "Mes prédictions sur l'année 2008 pour la compétition entre navigateurs") dont je parlais récemment est donc bel est bien lancée, j'adore quand les évènements me donnent raison.
2. L'équipe de l'IETeam reconnait **enfin** ses erreurs stratégiques du passé ( après plus de 10 ans!! ) et essaie tant bien que mal de corriger le tir pour le futur.
3. Comment se refiler une patate chaude ;) .
