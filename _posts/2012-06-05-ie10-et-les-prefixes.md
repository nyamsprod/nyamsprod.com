---
layout: post
title: "IE10 et les préfixes"
date: "2012-06-05"
categories: 
  - "web"
tags: 
  - "css3"
  - "ie10"
  - "prefixes"
---

La version finale de Internet Explorer 10 n'est pas encore sortie de chez Redmond mais on sait déjà que :

1. IE10 ne fonctionnera que sous Windows 7 (?) et 8;
2. IE10 n'est testable qu'avec une version test de Windows 8;
3. la IETeam vire les préfixes de toutes les propriétés CSS arrivées au status de Candidat à la Recommendation au W3C;
4. IE9 ne supporte aucune des propriétés qui _"roxent"_ en ce moment mise à part `-ms-transform`;

On peut donc en conclure que toutes les propriétés qui rendent vos sites _"shiny"_ (`animation`, `transition`, `transform`, `gradient`) fonctionneront dans IE10 sans préfixe. [Ce serait déjà le cas , parait-il, sous la dernière version de test (la 6ème du genre)](http://blogs.msdn.com/b/ie/archive/2012/05/31/windows-release-preview-the-sixth-ie10-platform-preview.aspx "Windows Release Preview: The Sixth IE10 Platform Preview").

Sachant que je fais parti de l'immense majorité des gens qui ne verront jamais les preview de IE10 avant sa sortie finale, je m'empresse de faire comme si les previews n'avaient jamais existées et je me permet donc de virer sans aucun état d'âme les préfixes `-ms-` pour les propriétés CSS ci-dessus mentionnées. Cela me fera gagner un ligne de code par propriété  (sauf, hélas, pour la propriété `transform`, à moins que IE9 ne soit mise à jour avec le patch qu'il faut, mais j'en doute ). Sachez que ce pas de nain est déjà un pas de géant dans l'éradication des préfixes _chiants(?)_ dans les code CSS.

_PS: le (?) à côté de chiant c'est juste pour l'autre débat sur l'opportunité des préfixes tout court en CSS et en JavaScript!!_
