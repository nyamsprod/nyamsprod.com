---
layout: post
title: "League\\Url 4 is out"
date: "2015-09-23"
categories: 
  - "web"
tags: 
  - "php-league"
  - "url"
---

I'm happy to announce that after more than 9 months of work [League\\Uri](http://url.thephpleague.com/) the follow up to League\\Url v3 is out.

This new version:

- comes with better URI RFC compliance;
- uses a simplified public API;
- introduces URI Modifiers for better interoperability;

This new version requires at least PHP 5.5.9 to work as intended and marks the end of support for League\\Url v3.

Let's take a tour of the new features and enhancements this package brings:

### A new namespace

Because this new version is a complete rewrite of the library, the package has been update to use a different namespace and a different [Composer package name](https://packagist.org/packages/league/uri) so that you can still use both v3 and v4 in the same project without running into dependency hell. This strategy will also allow you to migrate your code over time as needed but do keep in mind that v3 is no longer supported and only [bug fixes on the v4](https://github.com/thephpleague/uri) will be taken into account. You can install the last version by simply typing the code below in your composer installed box.

\[prism field=snippet\_url4\_composer\_install language=bash\]

### Stricter RFC compliance

The previous version was coded for usages in the PHP world only. This lead to bugs related to the package ignoring, for instance, basic RFC3986 rules.

To prevent theses issues to rise again but also to enable working with URIs created from applications outside of the PHP world, the new version makes a clear distinction between parsing and validating an URI. The package uses its own [URI](http://url.thephpleague.com/4.0/services/parser-uri/) and [query string](http://url.thephpleague.com/4.0/services/parser-query/) parsers to split the URI. And each URI object is responsible for making sure that its components are valid according its specific rules.

This process is enforced by the fact that each URI object is represented as a immutable value object, so any modification made to the URI object triggers the validation mechanism. \[prism field=snippet\_url4\_value\_object language=php\]

### Relation with PSR-7

Modern URIs are all based on [RFC-3986](http://http://tools.ietf.org/html/rfc3986) so instead of creating an interface for each specific URI scheme, the League URI objects implements a simple interface `League\Uri\Interfaces\Uri`. This interface only differs from the PSR-7 `UriInterface` interface in its docblock wordings to allow URI which do not support the HTTP and HTTPS schemes. This mean that if you are familiar with PSR-7 `UriInterface` you already know the public API of any League URI object.

### Supported URI Objects

Out of the box, the package implements URI objects for the following schemes:

- HTTP, HTTPS with the `League\Uri\Schemes\Http` class which implements the PSR-7 `UriInterface`;
- WS, WSS schemes with the `League\Uri\Schemes\Ws` class;
- FTP with the `League\Uri\Schemes\Ftp` class;
- Data with the `League\Uri\Schemes\Data` class;

But you can easily creates new URI objects for other schemes if you follow the [URI object creation guide](http://url.thephpleague.com/4.0/uri/extension/).

### URI Modifiers

Because we are dealing with immutable value objects and to enforce the package interoperability this version introduces URI modifiers. An URI modifier is callable which simplifies modifying URI objects in a sane and predicable way.

\[prism field=snippet\_url4\_modifier language=php\]

URI modifiers can also be use on PSR-7 Uri objects as well. The package comes bundle with more than 30 URI modifiers for common usages, but you are free and encourage to create your own URI modifier by following the [URI Modifier guide](http://url.thephpleague.com/4.0/uri/manipulation/#uri-modifiers).

### URI components revisited

Behind the scene, URI modifiers are powered by the package URI components classes which were improved. Their public API were simplified and just like URI objects, URI components are now immutable value objects. The goal was to enable better validation and manipulation of the component.

\[prism field=snippet\_url4\_path\_public\_api language=php\]

Of note, for each URI object defined in the package, you can access their respective components as objects using PHP's magic `__get` method.

\[prism field=snippet\_url4\_uri\_components language=php\]

### A new documentation website

Trying to cover all the changes in a single post would be overkill. So, instead, I recommend you take a look at [the documentation website](http://url.thephpleague.com/) which covers all the classes and services this new package introduce.

### Final note

Last but not least, the League\\Uri is an open source project with a MIT License so [contributions](https://github.com/thephpleague/uri/blob/master/CONTRIBUTING.md) are more than welcome and will be fully credited. These contributions can be anything from reporting an issue, requesting or adding missing features or simply improving or correcting some typo on the documentation website.
