---
title: "Deprecating a PHP Library"
date: "2016-02-22"
categories: 
  - "web"
tags: 
  - "deprecated"
  - "library"
  - "package"
  - "php"
  - "thephpleague"
  - "uri"
  - "url"
---

3 years ago, the first commit to what will become [the Url package](http://nyamsprod.com/blog/2014/handling-urls-with-leagueurl/) under thephpleague was pushed to github. The package goal was to handle HTTP URL in a consistent way in PHP applications. Since then, and through several releases as well as bug fixes the package has been well received by the community. But the more I applied some fixes to the package the more I came to the realization that the package needed a major rewrite. The rewrite started around a year ago and while trying to keep backward compatibility issues at minimum, it became clear during the process that this was not going to be possible. So to allow a better migration from one package to the other a new library named [URI was created](https://github.com/thephpleague/uri). To put it simple, URI is not just a fork or URL, it is the official successor to the URL package. And the naming change is not just a marketing stunt. URI is more flexible, it adds more features to handle any scheme specific URI in a more consistent way.

URI was released in September 2015 and the same day URL was marked as EOL  on its github page to clarify that no more development (bug and security fixes included) will be done around the package. Since then, however, according to packagist, URL has crossed the 200 000 downloads threshold and is being daily downloaded more that 500 times. In the meantime, URI is downloaded around 90 times per day and has recently crossed the 10 000 downloads on packagist. Is those numbers satisfying ? Should URI be more downloaded ? It all comes down to how one should deprecate an old package to make room for a new one.

In my case, I made one mistake. When URI was released I wrongfully called it Url v4. To me it made sense because the codebase was the same but the resulting message it sent was erroneous at best. It made using URL still okay even if URL was de facto abandoned. Since then, I've tried to correct this error. Both packages documentations have been separated and it is clearly mentioned on the [URL documentation website](http://url.thephpleague.com/) as well as on the github page, and on packagist too, that URL is EOL and that people should use [URI](http://uri.thephpleague.com) instead. And since today [URL is marked as abandoned on packagist](https://packagist.org/packages/league/url). Does it mean that because of theses actions the replace rate between both packages will increase ? I hope so but it will be a difficult task for 2 reasons.

The first reason is technical. Let's say a developer wants to switch from URL to URI but his/her PHP environment is incompatible with URI requirements, the developer is either using an unsupported version of PHP (PHP5.4-) or its code has an implicit dependency to URL through the use of a third party library. The good news is that if the user is on a supported version of PHP both packages can be used at the same time. Which means that the developer can upgrade his code without any breakage. But what about the third party library that as a developer you don't necessarily have access to ?  The more people upgrade to the latest stable PHP version the more third parties libraries will have an incentive for dropping old PHP versions and use URI instead of URL. Bottom line

https://twitter.com/nyamsprod/status/692721361509355521

The other reason is communication. Saying that URI is replacing URL is not enough. Stating that URI is better than URL is a better approach but again this is not enough _(URL and URI can work side by side)_. What one has to do is provide [information and examples](http://uri.thephpleague.com/examples/) to reach out to the PHP community and have them replace URL by URI because its the right thing to do. This is the most challenging part I would say, because as developers we are expected to have the skill to create and/or maintained code but we may not all have the required skills to sell (market) a product (a library) to a potential customer (the PHP developer community). The fact that URI is part of  [the php league](http://thephpleague.com/) which is a recognize brand does not make things easier on the contrary it means you should be as transparent as possible so that people relying on your works know what to expect. People are still downloading and using Guzzle3 despite countless advertisements about its deprecation for years now.

Tools and recommendations like semver, composer and packagist have made finding and following PHP packages simple. But that should not be an excuse to not take better steps to ensure everyone is getting the right information when it comes down to your package maintenance status and its inevitable deprecation. Everyday packages are created some will eventually become popular and grow but eventually they will all die. it is our responsibility as creator to make sure everyone is made aware of it at each stage of the package lifespan.
