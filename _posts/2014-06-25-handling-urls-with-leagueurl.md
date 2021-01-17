---
layout: post
title: "Handling URLs with League\\URL"
date: "2014-06-25"
categories: 
  - "web"
tags: 
  - "php-league"
  - "thephpleague"
  - "url"
---

While moving my CSV library over to [thephpleague](http://thephpleague.com/ "The League of Extraordinary Packages") group I happened to also move another simple library that I had built earlier called URL. As the name implied it was an attempt to ease URL manipulation in PHP.

A basic PHP installation comes with 3 powerful functions:

- `http_build_query` to transform an array into a query string
- `parse_str` that does the opposite and given a query string transforms it into a PHP array
- And last but not least `parse_url` to parse a given URL into its individual components

All these functions work fine but more than often you end up in situations when you have to add extra codes to completely deal with URLs. That's when `League\URL` comes handy.

I'm happy to say that a huge work was done behind the scene to clean up the code since the move and the result is a completely new library easier to use. The new library now:

- Treat FTPs URLs as well
- Treat Urls as well define value objects.
- Uses a common interface to access and manipule Url components classes to avoid [any code lingo](https://medium.com/@frankdejonge/a-case-against-coding-lingo-8ffae1a4fa4e "A case against coding lingo").
- Introduce a `\League\Url\UrlImmutable` object which is the immutable version of the `\League\Url\Url` class.

A very basic usage of the new library is as fellow:

```php
require 'vendor/autoload.php' //when using composer

use League\Url\Url;

$url = Url::createFromUrl('http://www.example.com');
$url->setPath('/path/to/index.php');
$url->setQuery(['location' => 'San Francisco']);
echo $url; // http://www.example.com/path/to/index.php?location=San%20Francisco;
echo $url->getBaseUrl(); // http://www.example.com
echo $url->getRelativeUrl(); // /path/to/index.php?location=San%20Francisco;
```

You can already found the library on [packagist](http://packagist.org/theleague/url "League\URL on packagist") and get the full documentation on [github](http://url.thephpleague.com/ "The Full Documentation"). Of course, you can always contribute by forking and making some pull request against the [github repository](https://github.com/thephpleague/url "League/Url source code")
