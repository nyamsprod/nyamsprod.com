---
layout: post
title: "On Uri validation"
date: "2016-05-04"
categories: 
  - "web"
tags: 
  - "php"
  - "programming"
  - "psr-7"
  - "rfc3986"
  - "the-php-league"
  - "uri"
  - "validation"
---

Yesterday a issue was created on [League\\Uri repo](https://github.com/thephpleague/uri/issues/56). Someone was asking if the Http URI object behavior was correct because the following code was emitting a `RuntimeException`.

{% gist 6ae0746abc4bd4140ac941d95ad3032e uri-validation-failed.php %}

In this post I'll explain the behavior observed in hope you'll get a better understanding of how the library works and how URI behave in general.

### URI are all the same...

Valid URIs must conform to [RFC3986](http://tools.ietf.org/html/rfc3986). This dense URI specification explains that an URI is composed of up to 8 components. Not all components are required to be present but at the very least an URI is composed of a path component which can be an empty string. To correctly parse any given URI according to the specification, the URI package comes with its own parser. Whenever you supply an URI string, the package first parse the string using its parser before feeding the results to an URI constructor. Let's see how this works

{% gist 6ae0746abc4bd4140ac941d95ad3032e uri-parsing.php %}

You may have expected the `example.com` part to be evaluated as the host component but since the authority delimiter (ie: `//`) was missing the parsing mechanism evaluates it as being part of the path component. This explains the output from using the `Http` class.

{% gist 6ae0746abc4bd4140ac941d95ad3032e uri-instance-comparison.php %}

### But scheme specific URI are all different...

RFC3986 specifies two things, how general URI must be created and how HTTP(s) specific URIs must be validated. The RFC emphasizes on the fact that **each scheme specific URI must have a separate RFC to specify how those URI should be validated**. For instance the validation rules for validating a [Data URI](http://uri.thephpleague.com/uri/schemes/data-uri/#validation) are not the same as the ones for validating [Web Sockets URIs](http://uri.thephpleague.com/uri/schemes/ws/#validation).

To take into account these specificities, every time a modification is made on a league URI object, the following validation steps are triggered:

1. we evaluate if the new component is valid.
2. we evaluate if the resulting URI is still valid according to scheme specific URI rules.

On failure, the first validation step will emit an `InvalidArgumentException` exception while the last one will throw a `RuntimeException` exception. Let's go back to our example:

{% gist 6ae0746abc4bd4140ac941d95ad3032e uri-validation-failed.php %}

The validation step which is failing is the last one. HTTP(s) specific URIs can not contain a scheme if no authority part is present. An authority requires at least a host component. Since no host component is present, adding a scheme resulted in an invalid URI.

Of note with the added authority delimiter the result is quite different.

{% gist 6ae0746abc4bd4140ac941d95ad3032e uri-validation-succeed.php %}

### Fin

Hopefully, this post has demystified how [the league URI package](https://github.com/thephpleague/uri) represents and handles URI in general and HTTP(s) URI in particular. Even though RFC3986 plays a pivotal role in URI definition and validation, it is not the only factor to take into account when dealing with URIs. You can always check [the package documentation website](http://uri.thephpleague.com/) for more informations on how to use the package.

[Uri](https://github.com/thephpleague/uri) is an open source project with a MIT License so contributions are more than welcome and will be fully credited.  These contributions can be anything from reporting an issue, requesting or adding missing features or simply improving or correcting some typo on the documentation website.
