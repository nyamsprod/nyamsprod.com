---
layout: post
title: "Handling CSV in PHP with Bakame.csv"
date: "2014-02-17"
categories: 
  - "web"
tags: 
  - "composer"
  - "csv"
  - "filtering"
  - "github"
  - "library"
  - "mit"
  - "open-source"
  - "parsing"
  - "php"
  - "psr-4"
  - "reading"
  - "semantic-versioning"
  - "writing"
---

For many years I've been struggling with CSV files. Not because they are difficult to parse, PHP has been able to manipulate those files since the days of PHP4 but because finding a clean, simple yet powerful library to handle them was a pain. So after many years of re-inventing the wheel every time I was confronted with parsing a CSV I've decided to take a step back and start writing my own CSV manipulation library. This is how [Bakame.csv](https://github.com/nyamsprod/Bakame.csv "Bakame.csv") came to be.

Now don't get me wrong [I looked on Github for similar libraries](https://github.com/search?q=csv+php "PHP CSV libraries on Github") but those that I've found were based on PHP4 stream functions or where not as documented or as straightforward as I wanted, some even had conflicted documentation or no documentation at all. So I started writing my own library in search of a well documented, powerful yet easy to of use library. If I had to point some of the goals achieve with this library I would say that:

- it is very light around 30k if you remove the examples and test folders;
- it uses SPL Iterator classes when possible to ease CSV filtering;
- it relies on SPL files classes to read and write CSV;
- it is very well documented with examples and all the code is fully unit tested;
- and last but not least It's open sourced on Github so anyone can contribute to it very easily;

As of this writing the library is on [version 4.2](https://github.com/nyamsprod/Bakame.csv/releases/latest "latest stable Bakame.csv version") but don't let the library version number fool you as the number only reflect the use of semantic versioning.

So please, don't be afraid to download the code, using composer, test it on your own CSV contents and if you find some bugs or some missing features please feel free to contribute to the library by opening an issue or by submitting a merge request with some new fancy cool improvements.
