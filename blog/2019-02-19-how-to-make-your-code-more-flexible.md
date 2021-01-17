---
title: "How to make your code more flexible"
date: "2019-02-19"
categories: 
  - "humeurs"
  - "web"
tags: 
  - "good-practice"
  - "open-source"
  - "php"
---

So I had a little exchange on the internet with the developers from [@spatie\_be](https://www.spatie.be). I've just discovered that they have a policy to never use final, private and void in their packages and when I ask why the answer was to enable flexibility in package usage.

https://twitter.com/freekmurze/status/1097606556617715714

Suffice to say I don't agree with this specific rule and even more so once I knew the reasoning behind its existence.

To illustrate why it is a bad guideline let's assume a PHP package containing the following class

\[gist id="ea48122e8082e480fd7cddbf4714cd3e" file="great.php"\]

Because this package is great and gets high praises from the internet of things it skyrocks on packagist and is downloaded so much so that someone picks it up and believe he/she can make it great again... no pun intended. How ? Well following said guideline he/she does the following :

\[gist id="ea48122e8082e480fd7cddbf4714cd3e" file="awesome.php"\]

Some folks stumble upon the new awesome package and decide to use it. Now without knowing they are all in a huge mess why ?

- If `Foobar\Great` updates its codebase and remove the `Great::internalMagic` method because why not ? `Awesome` is broken;
- If `Foobar\Great` adds a `doMore` method which returns something other than a `int`, `Awesome` is broken;
- If `self::MAGIC_NUMBER` constant is called in `Great::internalMagic ` instead of `static::MAGIC_NUMBER` the relation between both packages is broken;

Any non BC break action, according to semver, taken by the `Foobar\Great` will result in `Sunday\Dev\Awesome` having to check and review if nothing is broken and/or if its test suite is still working. I bet that at some point the `Sunday\Dev` maintainer will either open issues or completely fork the parent package in hope to resolve his own reported issues.

The root of all this is that both classes are so deeply bound to each others that their real API include public but also protected methods, properties and/or constants. Nothing can be changed or remove without triggering a BC break. You wanted flexibility you ended up with very tight coupling.

All that could have been avoided if the first class had been made final.

So we would have had:

\[gist id="ea48122e8082e480fd7cddbf4714cd3e" file="great-improved.php"\]

And:

\[gist id="ea48122e8082e480fd7cddbf4714cd3e" file="awesome-improved.php"\]

If `Foo\Great` is really as great as everyone think you can even improve its code and convert it into an interface if the need arise and add an implementation using a final class.

Bottom line, because final classes are closed to extensions they are way more flexible and less error prone as one may think at first glance. They provide a great starting point to improve control and maintenance over your code by embracing the composition over inheritance concept.  
That does not mean that inheritance is bad, but before using it on a concrete class ask yourself if the end result is not more harmful than creating a final class.

While some will view my examples as _too_ simplistic to favor my views and others may think that no good developer would do that or that I'm ranting on spatie packages let me end my post by reminding you the following:

First of all, I believe the [spatie open source packages](https://spatie.be/open-source) are great and I even contribute to some of them because like some of you I use some of their packages. Secondly, you'd be surprise how many other popular packages fail into this simple trap by overusing direct inheritance or other techniques like traits. Last but not least, I, myself, have been guilty of this in the past but I've since then learned my lesson and try to course correct things where and when I can and so should you :wink:
