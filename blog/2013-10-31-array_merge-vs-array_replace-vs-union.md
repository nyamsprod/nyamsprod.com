---
title: "array_merge vs array_replace vs union"
date: "2013-10-31"
categories: 
  - "web"
tags: 
  - "array_merge"
  - "array_replace"
  - "php"
  - "union"
---

This is just a reminder for me because I always struggle to find a good documentation:

When dealing with simple arrays without numeric indexes in PHP, there are 3 importants things to keep in mind:

1. The arguments order passed to the function or used with the `+` sign is important;
2. `array_merge` and `array_replace` are interchangeable since their results are identical;
3. the `+` sign gives the same results as `array_merge` and `array_replace` but the arguments order must be reverse;

**So performance wise, the `+` sign is better but beware or your arguments orders!!**

And here's a [little demo to make it clear to you](http://www.nyamsprod.com/test/array/ "Demo to demonstrate array_replace vs array_merge vs union in PHP")
