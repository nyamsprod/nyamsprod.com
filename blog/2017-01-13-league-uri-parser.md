---
title: "League Uri parser"
date: "2017-01-13"
categories: 
  - "web"
tags: 
  - "parser"
  - "parse_url"
  - "rfc3986"
  - "rfc3987"
  - "uri"
  - "url"
---

If you ever worked a lot with URLs you know that the first step before manipulating them is being able to correctly parse them into their different components. In PHP, this is accomplished using the [parse\_url](https://php.net/parse_url) function. But `parse_url` contains many bugs and shortcomings like:

- not being able to correctly parse an URL according to [RFC3986](https://tools.ietf.org/html/rfc3986)
- mangling URL [components](https://bugs.php.net/bug.php?id=68296)
- having even more [bugs and quircks](https://bugs.php.net/search.php?cmd=display&search_for=parse_url&x=3&y=5)

Theses issues are known to PHP's internals which is trying to solve them [by introducing a new URL parser, hopefully for PHP7.2](https://wiki.php.net/rfc/replace_parse_url). In the meantime, if correctly parsing the URL is crucial for you the PHP League is proud to announce the release of the [League URI Parser](https://packagist.org/packages/league/uri-parser).

The League URI Parser only works in PHP7+ and required [the intl extension](http://php.net/intl) to correctly parse RFC3987 URL's. Here's a simple example of how this parser works.

\[gist id="22752c39246544febd3e12b1b641da84" file="uri-parser.php"\]

As you can see, the parser returns an hash similar to `parse_url` so switching between them in your application should be straight forward.

Although the returned hash is similar, there are some key differences between this parser and `parse_url`. [The documentation](http://uri.thephpleague.com/5.0/parser/api/) goes into more in depth comparison between both parser but here's the main points:

- The parser always returns an array containing all the URL components;
- The parser makes a distinction between an empty component whose value is the empty string and an undefined one whose value is `null`;
- In case of an error, the parser will trigger an `InvalidArgumentException` instead of just returning `false`;

The League URI parser also provide a method to validate any host string. This method is capable of validating a:

- Host as an IP string (IPv4 and IPv6)
- Host as registered name

\[gist id="22752c39246544febd3e12b1b641da84" file="host-validator.php"\]

Regardless of the parser you will end up using for your next application, do keep in mind that parsing and validating an URL are two different actions. For instance, if you go back to the first example provided, the returned URL is invalid against the rules of a [data URL scheme](https://tools.ietf.org/html/rfc2397), but parsing was correct.

### Final note

The [League Uri Parser](https://github.com/thephpleague/uri-parser) is an open source project with a MIT License so contributions are more than welcome and will be fully credited. These contributions can be anything from reporting an issue, requesting or adding missing features or simply improving or correcting some typo on the documentation website.
