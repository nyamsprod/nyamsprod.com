---
title: "Formatting a Date in PHP the right way"
date: "2016-06-15"
categories: 
  - "web"
tags: 
  - "date"
  - "datetime"
  - "formatting"
  - "i18n"
  - "intl-extension"
  - "php"
  - "setlocale"
  - "strftime"
---

Lately I've been doing some translation in PHP and one of the main issue was to translate a date into a human readable string according to the user settings.

Historically, in PHP people have been using a conjunction of `strftime` and `setlocale` to achieve this goal. like in the following example:

\[gist id="cc5e9692284864a6a20345a47c4a536f" file="dateformatting-strftime.php"\]

This example has many problems:

The string you have to give `setlocale` depends on the locale that exists on your platform. For instance on _Ubuntu_ if I specify `fr_FR` instead of `fr_FR.UTF8` the result may differ depending on the installed locales. You could come up with a detection function prior to use `setlocale` but then you add even more burden in the locale detection.

Another problem is that if you only want to convert one specific date and nothing else the code should then be:

\[gist id="cc5e9692284864a6a20345a47c4a536f" file="dateformatting-setlocale.php"\]

As you can see, `setlocale` affect your environment so using it should not be the recommend way. So what is the alternative ?

Well since PHP5.5 the [Intl extension](http://php.net/manual/en/book.intl.php) introduce the [`IntlDateFormatter::formatObject`](http://php.net/intldateformatter.formatobject) static method. This method addresses all the previous usage limitations. here's an example:

\[gist id="cc5e9692284864a6a20345a47c4a536f" file="dateformatting-intl.php"\]

- The method expects a `DateTime` object which means that the object timezone is taken into account. This was not the case with `strftime`.
- [The formatting string follows the UCI standard](http://www.icu-project.org/apiref/icu4c/classSimpleDateFormat.html#details) which make them understandable not only by PHP users.
- You can specify the locale per function call so no more changing your environment inside your code.
- The locale string is also platform independent. Which means that no extra prefix or requirement is needed to make this code works.

The only drawback that I could spot was that `DateTimeImmutable` also introduced in PHP5.5 is not yet supported by the method despite [a bug for its support being filled since 2013](https://bugs.php.net/bug.php?id=65683).

To put it simple, if you need to format a Date in PHP please use the Intl extension whenever you can.
