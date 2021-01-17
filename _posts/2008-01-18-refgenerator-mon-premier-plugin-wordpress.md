---
layout: post
title: "RefGenerator, mon premier plugin Wordpress"
date: "2008-01-18"
categories: 
  - "web"
tags: 
  - "css-layout"
  - "javascript"
  - "plugin"
  - "refgenerator"
  - "wordpress"
---

**Attention une nouvelle version du plugin est maintenant [téléchargeable](http://nyamsprod.com/blog/refgenerator/).**

Après avoir créé un template quasiment _from scratch_ pour mon blog, je me suis dis que je ne m'arrêterais pas en si bon chemin et j'ai donc écris mon premier [plugin Wordpress](http://codex.wordpress.org/Plugin_API "Comment créer un plugin Wordpress"). En fait je pourrais faire facilement 5 articles pour expliquer comment RefGenerator a été écrit mais je n'ai pas le temps pour l'instant. Peut-être qu'un autre jour j'expliquerais ma démarche, mais pas aujourd'hui, pas maintenant.

### La conception

Généralement, lorsque je code un script ou une application, je me demande toujours si

1. cela vaut la peine ;
2. cela n'a pas déjà était fait ;
3. et finalement si j'ai les reins solides pour commencer et surtout finir ce que j'ai entamer ;) ;

Pour ce script, il m'a fallu réellement 3 jours (pas à 100%) pour le coder mais près de 2 à 3 mois pour vraiment me mettre en condition pour le réaliser. Au début ce n'était qu'une extension de mon template, et maintenant c'est un plugin totalement indépendant de celui-ci et ça c'est cool. Cela veut dire qu'il est utilisable par n'importe qu'elle blog Wordpress 2+.

### RefGenerator

Bon trèves de bavardage, à quoi sert RefGenerator ? **C'est un plugin 2 en 1** qui sert à lister en fin d'article tous les liens externes utilisés dans celui-ci. En fait, il génère la liste des réfèrences externes utilisées pour écrire votre article, et l'ajoute en fin d'article trier dans l'ordre d'apparition du lien dans l'article.

Pourquoi est-ce un plugin 2 en 1 ? Tous simplement par ce que RefGenerator peut être utilisé de 2 manière distinctes, via PHP ou via le javascript pour générer la liste des références. Chacune de ces méthodes ayant des avantages et des inconvénients.

Est-ce que ce plugin est pour moi ? Cela dépend de la finalité de votre blog et surtout de votre besoin ou non d'un tel plugin. Personnellement je l'ai développé parce qu'on me la demandé gentiment et que je voulais comprendre comment fonctionner les plugins sous Wordpress. Du coup, j'ai retiré l'extension de mon template et je l'ai ré-implanter via RefGenerator dans mon blog.

### Comment ça marche

1. Télécharge le fichier compressé qui se trouve en fin d'article et décompresse-le sur ton ordinateur.
2. Transfert le dossier décompressé dans le répertoire `plugins` de ton installation wordpress.
3. Rend-toi ensuite dans la partie administration de ton wordpress, dans l'onglet Plugins et active RefGenerator.
4. Puis, toujours dans la partie administration sous l'onglet Options de Wordpress clique sur le sous-onglet RefGenerator qui vient de se rajouter.
5. Configure RefGenerator en fonction de la méthode utilisée pour générer la liste des liens externes de tes articles.

### Quelle méthode choisir ?

Si vous venez d'installer Wordpress et que vous n'avez pas l'habitude de bidouiller dans les templates, la méthode PHP vous conviendra, _c'est le cas, je pense, de la majorité des gens qui vont télécharger ce plugin_. En revanche, si vous êtes un utilisateur chevronné de Wordpress et que modifier vos templates ne vous fait pas peur, alors la méthode javascript vous sera plus utile. Quelque soit la méthode utilisée, j'espère que le plugin répondra positivement à vos attente.

### Last but not least

Si vous changer le nom de l'attribute `class` de la balise qui contient la liste de liens, n'oubliez pas de modifier les fichiers CSS qui se trouvent dans le sous dossier `css` du répertoire du plugin. Veuillez trouver ci-dessous le dossier compresser de refGenerator au format `zip` et au format `tgz`, choisissez le format de compression que vous préférez.

**Attention une nouvelle version du plugin est maintenant [téléchargeable](http://nyamsprod.com/blog/refgenerator/).**

La page d'administration du plugin contient des fautes d'orthographe du à mon empressement à sortir le plugin. Pour traduire dans votre langue le plugin, il vous suffit. de vous rendre dans le dossier `langs` dans lequel vous retrouverez les fichiers de langues. Si vous avez l'âme d'un professeur de français, Vous devez d'abord copier le fichier (.po) en le renommant en fonction de votre langue et corriger les fautes d'orthographe et ensuite mettre à jour son fichier .mo via la commande `[msgfmt](http://fr.wikipedia.org/wiki/Gettext "explication de la traduction dans Wordpress") refgen-xx_XX.po -o refgen-xx_XX.mo` sous Unix/linux/BSD ou en utilisant [PoEdit](http://www.poedit.net/download.php "PoEdit : Programme de traduction de logiciels libres") sous Windows. Le suffixe `xx_XX` est l'identifiant de la langue de votre Wordpress. Envoyez-moi les fichiers modifiés et je mettrai à jour RefGenerator le plus rapidement possible pour la joie de tous.
