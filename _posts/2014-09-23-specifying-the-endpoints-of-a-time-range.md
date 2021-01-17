---
layout: post
title: "Specifying the endpoints of a time range"
date: "2014-09-23"
categories: 
  - "web"
tags: 
  - "bakame"
  - "datetime"
  - "github"
  - "mysql"
  - "period"
  - "range"
---

In PHP we hate re-inventing the wheel so when I stumble on [Mathias Verraes post about a ReportingPeriod](http://verraes.net/2014/08/resolving-feature-envy-in-the-domain/ "Resolving Feature Envy in the Domain") class it just reminded me how often I came across the same problem over and over again in my daily life as a developer. So to resolve this issue, hopefully, once for all, I decided to implement an Immutable Value Object class which will deal with time range. So here I present you [`Bakame\Period`](https://github.com/nyamsprod/Period "Bakame\Period a Simple PHP Class to manipulate Time Range")

If you look at the [Github source code](https://github.com/nyamsprod/Period/blob/master/src/Period.php "Bakame\Period source code"), you'll see that the class is very simple and only requires PHP 5.3+ . The only problem that I run into when creating this class was specifying its endpoints values.

To understand the solution that I implemented I'll take two examples:

First let's assume you are booking your holidays so you need to tell your boss when you will be back at work. You have at least two options to say it:

> I'll take my holiday from January 1st to January 7th included.

Or

> I'll take my holiday on January 1st and I'll be back at work on the 8th of January.

Both sentences convey the same information but note that in the first one you had to add the _**included**_ word in your statement to remove any ambiguity. Otherwise, your boss would have think that you would be back at work on the 7th of January. Telling your boss the real end of your holiday is not always a smart move :) .

Now let's look at another situation that will talk more to us developers (..because developers never take holidays). Look at the following queries.

```php
$query1 = "SELECT COUNT(*) FROM users WHERE create_at>= '201-06-05 00:00:00' AND create_at <= '2014-06-05 23:59:59'";
$query2 = "SELECT COUNT(*) FROM users WHERE create_at>= '201-06-05 00:00:00' AND create_at < '2014-06-06 00:00:00'";
```

- The first query uses endpoints included in the interval;
- The second query uses the included endpoint for the range beginning but the excluded endpoint for the range end.

Both queries seem to return the same value but in reality they don't. if your SQL engine supports micro-seconds which I think it already does [in recent versions of MySQL](http://dev.mysql.com/doc/refman/5.6/en/fractional-seconds.html "MySQL supports fractional seconds since version 5.6.4"), for instance, you will be missing some microseconds in your query. So if these queries return the same value in your SQL engine, it's only because of an implementation limitation not because they should in the first place !! (As a side note this is why I hate using the BETWEEN statement in MySQL queries when dealing with date fields).

In summary, to be on the safe side of time range manipulation it is better to specify:

- the included starting time as one endpoint;
- the excluded ending time as the other endpoint;

Even if it may sound odd in the beginning after some usages you'll feel that the tradeoff is far less important than the clarity and usage gain. And that's why when using `\Bakame\Period` objects you'll notice the following behaviour.

```php
<?php
use Bakame\Period; 
$period = Period::createFromMonth(2014, 10);
$period->getStart(); //returns new DateTime('2014-10-01');
$period->getEnd(); //returns new DateTime('2014-11-01');
$period->contains($period->getStart()); //return true;
$period->contains($period->getEnd()); //return false;
```

Happy time range manipulation with `Bakame\Period`!!
