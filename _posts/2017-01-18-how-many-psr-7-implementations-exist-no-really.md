---
layout: post
title: "How Many PSR-7 Implementations Exist? No really"
date: "2017-01-18"
categories: 
  - "humeurs"
  - "web"
tags: 
  - "composer"
  - "packagist"
  - "psr-7"
  - "psr7"
---

[Paul M Jones](http://paul-m-jones.com/archives/6510) wrote a blog post around [PSR-7](http://www.php-fig.org/psr/psr-7/) implementations and even though his response was zero I was intrigued by [packagist results](https://packagist.org/providers/psr/http-message-implementation). Since I am maintaining an implementation of [PSR-7 `UriInterface`](http://uri.thephpleague.com/5.0/uri/schemes/http/), I was curious to see despite his opinion how many different implementations really exists and their _quality_.

So looking a the numbers of implementations, I thought it would take me hours to go through the list but I was wrong. The packages found can be quickly divided in 4 categories:

- The first category represents **cheating developers.** The package maintainer just copy/paste a famous implementations (usually _Diactoros_) and just changed the namespace or aliased it and claimed that it is a complete implementation. Without going into copyright or infringement I'm baffled at how someone could do that, publish it and claim it as his/her work or think that he/she could benefit from it.
- The second category represents **cheating packages** that advertise themselves as implementing PSR-7 while in reality they just don't. When you look at the code source you will found  no traces whatsoever of PSR-7 except that they claim to provide such feature. Again another strange technique to promote, someone package.
- In the third category you'll find packages which are really badly written. They do require the PHP-FIG interfaces and implement them. But the code quality is so bad anyone downloading or using them are really doing themselves a bad service.
- Last but not least their are the good, quality tested package like _Slim_, _Diactoros_ or _Guzzle_ and packages that just require them to work. This does not mean that those packages do not contain bugs or shortcoming but by reading the code and looking at the test suite you directly spot the code quality.

### TL;DR

The sheer number of PSR-7 implementations is a false promise. Don't believe a book by its cover. Whatever a library or a package advertises, first look at its code and try to measure the package quality before using it. Using _Composer_ and being on _Packagist_ is so common nowadays that it should **never** be taken as a quality measure.
