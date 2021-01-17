---
layout: post
title: "A class to generate URI Template in PHP"
date: "2020-01-29"
categories: 
  - "web"
tags: 
  - "php"
  - "thephpleague"
  - "uri"
  - "uri-template"
---

Ever since I released the `League\Uri` package I always wanted to add an URI template class in it. But I never felt having to write one because I never used the URI template feature myself and the only time I had to do it I used the implementation that came bundle with the `Guzzle` library. It turns out that `Guzzle's` maintainers have decided to drop their own implementation for the next `Guzzle` major release which is in beta release as of this writing. And since I was in need of such feature I finally got around to add the functionality to the `League\Uri` library.  
In this post I would like to introduce the `League\Uri\UriTemplate`, the main new feature of `League\Uri 6.1`.

For starter, like most of the other classes included in the library the `League\Uri\UriTemplate` follows a known RFC which is [RFC6750](https://tools.ietf.org/html/rfc6570). This RFC describes how to interpolate and expand a template so that its result is a fully compliant URI as described in [RFC3986](https://tools.ietf.org/html/rfc3986).  

## Using the template

While the core expansion logic is based on the `Guzzle` 6.5 implementation, its public facing API is a combination of the main Python and Java implementations.

{% gist 7eeee674eb64e8384637e9c07239d3b7 uri-template-basic-usage.php %}

The advantage of this public API versus the one that was used in the `Guzzle` implementation is that with one object you can create an infinite number of URI instance by just changing your variables on each `UriTemplate::expand` calls. The template is parsed only once on instantiation.

## Using the variables

Another nit trick is that you can define default variables on the constructor  

{% gist 7eeee674eb64e8384637e9c07239d3b7 uri-template-with-default-variables.php %}

In the example above, the `version` variable is applied without you having to fill it in the when calling the `expand` method. Keep in mind, that to give you more flexibility the default variables can still be overwritten if the same variables are used with the `expand` method.

{% gist 7eeee674eb64e8384637e9c07239d3b7 uri-template-with-default-variables-overwritten.php %}

## Interoperability

To enable better interoperability with other implementations in other languages, the class was design using an independent [URI template test suite](https://github.com/uri-templates/uritemplate-test) for expansion conformance. So while updating the implementation I made sure to always pass this independent test.  
  
In order to do so, under the hood, the class does lots of validations on instantiation and when using the `expand` method to make sure:

- the template syntax is conformed to the RFC;
- the variable syntax is not forbidden by the RFC;
- the resulting expansion produces an RFC compliant URI instance;

Some optimisations are also introduced to lazy cache template expansion in case no variable and/or no expression are presents.

## Alternative

If you already worked with URI Template in PHP you probably came across the [rize/uri-template](https://github.com/rize/UriTemplate) library. The main differences between both implementations apart from the public API are that the latter offers features that are not covered by the RFC, and thus, are not present in this class. Namely an extraction feature which returns the possible variables used in a valid URI and an extension to add the ability to expand URI using `http_build_query` type parameters.

## Final note

The [League/Uri](https://github.com/thephpleague/uri) is an open source project with a MIT License so contributions are more than welcome and will be fully credited. These contributions can be anything from reporting an issue, requesting or  
adding missing features or simply improving or correcting some typo on the documentation website.

And if you appreciate the work and the effort put in the library you can also [sponsor me](https://github.com/sponsors/nyamsprod) to enable me to continue to fix and improve the library.
