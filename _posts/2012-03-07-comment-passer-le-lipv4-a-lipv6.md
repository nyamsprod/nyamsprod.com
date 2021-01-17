---
layout: post
title: "Comment passer le l'IPv4 à l'IPv6"
date: "2012-03-07"
categories: 
  - "web"
tags: 
  - "ipv4"
  - "ipv6"
  - "mysql"
  - "php"
  - "reseau"
---

Pense bête personnel pour me rappeler ce que je dois faire avant le 6 Juin lorsque [le monde basculera](http://www.pcinpact.com/news/68388-ipv6-launch-day-deploiement-societes.htm "le 6 Juin déploiement massif de l'IPv6") ...

1. Niveau MySQL:
    - A partir de la version 5.6.3 je peux utiliser [les fonctions natives](http://dev.mysql.com/doc/refman/5.6/en/miscellaneous-functions.html#function_inet6-aton "MySQL IPv6 functions");
    - Avant je dois [installer  les User Defined Functions](http://labs.watchmouse.com/2009/10/extending-mysql-5-with-ipv6-functions/ "UDF for IPv6 support in older MySQL servers") si possible;
    - Stocker les adresses IPv6 dans [un champs du type VARBINARY](http://dev.mysql.com/doc/refman/5.0/fr/binary-varbinary.html "Les type VARBINARY dans MySQL 5.0");
2. Niveau PHP:
    - A partir de la version PHP5.1, utiliser les fonctions [inet\_ntop](http://www.php.net/manual/en/function.inet-ntop.php "inet_ntop : IPv6 PHP function") et [inet\_pton](http://www.php.net/manual/en/function.inet-pton.php "inet_pton : IPv6 PHP function")
