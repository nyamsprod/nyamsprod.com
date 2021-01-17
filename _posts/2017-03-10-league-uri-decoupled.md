---
layout: post
title: "League Uri decoupled"
date: "2017-03-10"
categories: 
  - "web"
tags: 
  - "decoupled"
  - "middlewares"
  - "parse_str"
  - "parse_url"
  - "thephpleague"
  - "uri"
---

Last month the release of League\\Uri version 5 was announced using a simple tweet.

https://twitter.com/nyamsprod/status/828530046172332032

While I pointed out in the tweet that this new release is PHP7 only, the main selling point of this new version is the package conversion into a meta-package. So instead of one single release, last month 5 packages were in fact released.

- [League\\Uri-Interface](https://github.com/thephpleague/uri-interfaces) a basic Uri Interface
- [League\\Uri-Parser](https://github.com/thephpleague/uri-parser) a RFC3986/RFC3987 URI parser
- [League\\Uri-Components](https://github.com/thephpleague/uri-components) the URI components package
- [League\\Uri-Schemes](https://github.com/thephpleague/uri-schemes) which validate and normalize any URI according to its scheme specificity
- [League\\Uri-Manipulations](https://github.com/thephpleague/uri-manipulations) which manipulate URIs through a formatter and a collection of URI middlewares

By splitting the main package into smaller packages the end user can now select the packages he/she really more easily. For instance, if you already are using a PSR-7 `UriInterface` compliant object, you only need to require the `league\uri-manipulations` to perform the following operation.

{% gist 48814c42143a27b9b9491c3c76fa74cb uri-middleware.ph %}

As a side note, this change also enables easier maintenance as bugs can be more quickly fix in each separate package.

Of course, a new major release means [improvements](http://uri.thephpleague.com/5.0/) and [backward incompatible changes](http://uri.thephpleague.com/upgrading/5.0/) in the public API. For instance, a new `Query::getParams` method is introduced to improve query string deserialization made by PHP's `parse_str`. This method:

- [will not mangle the returned data](https://wiki.php.net/rfc/on_demand_name_mangling);
- [is not bound by PHP ini settings](http://grokbase.com/t/php/php-internals/123epc6d2m/let-parse-str-parse-more-than-max-input-vars-args);
- [allows better control over the serialization](https://bugs.php.net/bug.php?id=52343);

{% gist 48814c42143a27b9b9491c3c76fa74cb query-getparams.php %}

If you are still using `League\Uri 4.x` do not worry. The package remains supported for 6 more months through patches and security fixes. But new features will only land on the respective new packages.

Because trying to summarize 5 packages into a single blog would be overkill I'd suggest you head over the new [documentation website](http://uri.thephpleague.com) for more informations.

### Final note

The [League Uri](https://github.com/thephpleague/uri) is an open source project with a MIT License so contributions are more than welcome and will be fully credited. These contributions can be anything from reporting an issue, requesting or adding missing features or simply improving or correcting some typo on the documentation website.
