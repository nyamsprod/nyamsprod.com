---
layout: post
title: "DatePeriod demystified"
date: "2016-05-12"
categories: 
  - "web"
tags: 
  - "dateinterval"
  - "dateperiod"
  - "datetime"
  - "datetimeimmutable"
  - "php"
---

Have you ever wanted to work with PHP's `DatePeriod` object. This object introduced in PHP 5.3.0 enables iterating over a set of dates and times (ie datepoints), recurring at regular intervals, over a given time range. In practice, on instantiation this object produces a `Traversable` that generate `DateTimeInterface` objects. This can be helpful, for instance, if you want to produce data reports at specific datepoints over a time range.

The easiest way to instantiate such object is to give the constructor a starting and an ending datepoints as well as the interval between each recurrence.

{% gist 85fb8c47a1dbe06602a6 dateperiod-datetime.php %}

By default the ending datepoint is not returned and you can further exclude the starting datepoint by using the class constant `DatePeriod::EXCLUDE_START_DATE`.

With the introduction of the `DateTimeImmutable` object in PHP5.5, and a subsequent bug fix to `DatePeriod` in PHP5.5.8, the object results became rather interesting. To sum it up, when iterating over a `DatePeriod`, the datepoint returned is of the same instance as the starting datepoint. Let's illustrate this by taking the first example and using a `DateTimeImmutable` object instead as the starting datepoint.

{% gist 85fb8c47a1dbe06602a6 dateperiod-datetimeimmutable.php %}

Iterating the `DatePeriod` will now return `DateTimeImmutable` objects instead.

Now that we understand how the iteration works, we need to know how to get informations about an already instantiated `DatePeriod` object ?

`DatePeriod` exposes its properties using two distinct API that share a common trait, [they are **undocumented**](http://php.net/DatePeriod).

If you are on PHP5.6.5+ you **should** use the recommend API

{% gist 85fb8c47a1dbe06602a6 dateperiod-property-api.php %}

If you are using an older version of PHP, you _may_ use the fact that `DatePeriod` exposes a copy of its internal state.

{% gist 85fb8c47a1dbe06602a6 dateperiod-buggy-api.php %}

The latter API is buggy for different reasons:

- The datepoint value does not returns the instance expected. In the example we gave it a `DateTimeImmutable` object yet start returns a `DateTime` object
- The returned `DateInterval` object is in an invalid state and no usable.
- No HHVM version supports this API.

What to take from this ?

1. Always rely on the interface meaning if an object is said to return a `DateTimeInterface` do not try to use methods or property outside of the intended interface as the result may be unexpected.
2. Upgrade you PHP's installation to the latest stable version when possible

**Post Scriptum:** If you want to further manipulate your time range in PHP, I would recommend the use of [Period](http://period.thephpleague.com/api/). This library, I maintain, is part of [the PHP league](http://thephpleague.com). Period is composed of a single class that handles time range in a uniform and predicable way. The class which comes with many useful named constructors, compares and modifies time range easily by being an immutable value object just like the `DateTimeImmutable` object.

[League\\Period is an open sourced project on Github](https://github.com/thephpleague/period), and is easily available using composer. You are, of course, welcome to contribute to the source code to improve it.
