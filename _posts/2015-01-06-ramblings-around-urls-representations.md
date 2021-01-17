---
layout: post
title: "Ramblings around URLs representations"
date: "2015-01-06"
categories: 
  - "web"
---

https://twitter.com/nyamsprod/status/552031046527889408

As I am working on the next version of the [League\\URL package](http://url.thephpleague.com "The League\URL package"), I reached a point where a BC break must be done around the URLs classes. In the current stable version (version 3), the URLs can be treated as mutable or immutable objects. This means that depending on your needs you may choose to represent your URLs one way or another. To keep the package tight and simple my approach was to introduce an [`URLInterface`](https://github.com/thephpleague/url/blob/3.2.1/src/UrlInterface.php "The League\Url\UrLInterface in version 3.0") interface that both classes could share. This simple approach introduced a major problem that need to be address in the next version.

To understand the issue let's illustrate it with the following code:

First, let's write a simple code using the mutable version of the URL class.

\[prism field=snippet\_simple\_url\_setter language=php\]

Now, let's rewrite the same code using the immutable version.

\[prism field=snippet\_simple\_urlimmutable\_setter language=php\]

The root of the problem is that while both code follow the same interface the end result is quiet different. So only relying on the `URLInterface` interface is not enough to represent how update made to an URL are applied. This may even break someone code if the developer typehint on the interface only, which is what the interface was supposed to be used for.

A way to reduce this issue is to:

- rename modifying methods in the immutable version to distinguish them from the mulable version.  To this end, I have replace by `with`  the `set` prefix on all the modifying methods of the immutable version.
- remove the fluent interface from the mutable URL version.
- reduce the `URLInterface` to shared getter methods so that both class can continue to follow the same interface.

Unfortunately, this does not solve the issue. As seen with the following snippets, the issue is jut less visible:

Let's write another simple code

\[prism field=snippet\_complex\_url\_setter language=php\]

Now let's rewrite the same code using the immutable version.

\[prism field=snippet\_complex\_urlimmutable\_setter language=php\]

The only way out of this is to simply drop one of the URLs class. And as I write these lines I'm leaning toward removing the mutable URL class, why ?

URLs are string representation of a location:

- If you only change one character from one of its components you gain a whole new URL.
- To be considered valid, an URL need to have all its components valid.
- The URLs components may be loosely independent from each other but their meaning/representation can only be fully understood when being part of a complete URL.

So URLs are good candidate to being immutable value object. Treating URLs as being immutable does not remove any of the current features expose by the package they still all remains the same, but you gain clarity of intent whenever you access/modify the URL. The only drawbacks that I could find so far are:

- You may need more lines of code to update an URL object. This issue may be resolve by using a proxy of some kind for the most obvious operations.
- Developers may think of the _new_ URL class as being a simple builder.

\[prism field=snippet\_new\_url language=php\]

So what do you think ? Your feedbacks are welcomed.
