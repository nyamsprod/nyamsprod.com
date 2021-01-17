---
layout: post
title: "Dealing with date and time in modern PHP"
date: "2014-11-19"
categories: 
  - "web"
tags: 
  - "carbon"
  - "date"
  - "dateinterval"
  - "dateperiod"
  - "datetime"
  - "datetimezone"
  - "mktime"
  - "period"
  - "php"
  - "strtotime"
---

Any PHP application has to deal at some point with date and time and there are so many ways to get it wrong in PHP that I thought I would give some tips on how to properly handle them in modern PHP. My post will assume that you are using the currently stable release of PHP, which is at the time of writing _PHP 5.6_. That being said I'll indicate for each advice the minimum PHP version required to start using it.

## Configuring your PHP environment

You should always make sure you control your application timezone settings. To do so, since PHP 5.1, you can use the [date\_default\_timezone\_set](http://php.net/date_default_timezone_set "date_default_timezone_set on php.net") function. Of note, since PHP5.3, if you do not properly set the timezone of your application an `E_WARNING` alert will be throw.

Of course, you can always at any given time retrieve your current setting with the [date\_default\_timezone\_get](http://php.net/date_default_timezone_get "date_default_timezone_get on php.net") function.

```php
<?php
//ideally in your application bootstrap before anything else
date_default_timezone_set('Africa/Kinshasa');
echo date_default_timezone_get(); //displays 'Africa/Kinshasa'
```

If there's one thing to take away from this post is that not knowing or incorrectly setting your environment will always result on unexpected bugs no matter what you do.

**NB: This is a good time to also check that your back-end (database, filesystem, ...) is also correctly set to further avoid bugs when saving/retrieving data from it**

## PHP Internal solutions

Prior to PHP 5.2, the language dealt with date and time using at least 4 functions.

- [time](http://php.net/time "time on php.net")
- [date](http://php.net/date "date on php.net")
- [mktime](http://php.net/mktime "mktime on php.net")
- [strtotime](http://php.net/strtotime "strtotime on php.net")

Since then, PHP has mature and offers [a complete set of classes](http://php.net/datetime "Date and Time Book on php.net") to properly deal with date and time. Once you'll start using them you will never want to use the _older_ mechanism again. Here's the complete list of classes and the PHP version they were introduced in:

- [DateTimeZone](http://php.net/class.datetimezone "DateTimeZone on php.net") _since PHP 5.2_
- [DateTime](http://php.net/class.datetime "DateTime on php.net") _since PHP 5.2_
- [DateTimeImmutable](http://php.net/class.datetimeimmutable "time on php.net") _since PHP 5.5_
- [DateInterval](http://php.net/class.dateinterval "DateTimeInterval on php.net") _since PHP 5.3_
- [DatePeriod](http://php.net/class.dateperiod "DatePeriod on php.net") _since PHP 5.3_

With these 5 classes anything can be done around dates, time and time ranges. Since this post is about tips, you should refer to the PHP Documentation website to understand how they work.

To be fair, you will mostly work with the `DateTime` class. But knowing how and when to use the other classes is as fundamental as you will most likely need them at some point in your development. You should keep in mind the following tips:

- There is no `__toString` method attached to any of these classes.
- For modifying methods `DateTime` uses a fluent interface **since PHP 5.3**.
- When creating a new `DateTime` object if no `DateTimeZone` is specified, the object will fallback to the timezone specified by `date_default_timezone_set`.

```php
<?php
date_default_timezone_set('Africa/Douala');
$dt1 = new DateTime('2014-10-12 14:23:13');
$dt2 = new DateTime('2014-10-12 14:23:13', new DateTimeZone('Africa/Nairobi'));
echo $dt1->format(DateTime::W3C), PHP_EOL; //2014-10-12T14:23:13+01:00
echo $dt2->format(DateTime::W3C), PHP_EOL; //2014-10-12T14:23:13+03:00
```

- You can compare two `DateTime` objects directly using standard comparison.

```php
<?php
$dt1 = new DateTime('-1 HOUR'); 
$dt2 = new DateTime('+3 DAYS'); 
if ($dt1 > $dt2) {
    echo 'dt1 is greater than dt2', PHP_EOL;
} elseif ($dt1 < $dt2) {
    echo 'dt1 is less than dt2', PHP_EOL;
} else {
    echo 'dt1 equals dt2', PHP_EOL;
}
```

- The difference between two `DateTime` objects is expressed as a `DateInterval` object.

```php
<?php
date_default_timezone_set('Africa/Douala');
$dt1 = new DateTime('-1 HOUR');
$dt2 = new DateTime('NOW', new DateTimeZone('Africa/Nairobi'));
$diff = $dt1->diff($dt2); //$diff is a DateInterval object
echo $diff->h; //display '1'
```

**Since PHP 5.5** `DateTime` and `DateTimeImmutable` implements the same `DateTimeInterface` interface and exposed the same methods. You can compare, and expressed the difference between objects of both class like previously shown.

The main difference between both classes is that `DateTimeImmutable` is a immutable value object. This means that for all modifying methods a `DateTimeImmutable` object always returns a new modified copy of itself while a `DateTime` object modifies itself.

```php
<?php
$dt = new DateTime();
$dtim = new DateTimeImmutable();
$dtim == $dt; //returns true
$dt->add(new DateInterval('PT1H')) //adding a 1 hour interval
    ->sub(new DateInterval('P3D')); //removing an interval of 3 days
$newDtim = $dtim->add(new DateInterval('PT1H'))
            ->sub(new DateInterval('P3D'));
$newDtim == $dt; //returns true
$dtim == $dt; //returns false because $dt has changed NOT $dtim
```

For time ranges you can use the `DatePeriod` class. It generates `DateTime` objects contained within a specific time range at a given interval.

- When creating a `DatePeriod` with an end datetime, the latter is excluded from the generated time range.

```php
<?php
$end = new DateTime('+4 DAYS');
$period = new DatePeriod(
    new DateTime('TODAY'),
    new DateInterval('P1D'),
    $end
);
$res = iterator_to_array($period, false);
echo count($res); //returns 5;
array_pop($res) != $end; // returns true;
```

- Alternatively, you can create a `DatePeriod` class using **recurrences** not **occurences** to indicate the number of `DateTime` objects to be generated.

```php
<?php
$period = new DatePeriod(
    new DateTime(),
    new DateInterval('P1D'),
    3 //recurrences
);

echo count(iterator_to_array($period, false)); //return 4;
```

## Open source solutions

I have to admit, sometimes, working with the above classes can be tricky. This is where the PHP Open Source Community comes handy. So instead of trying to reinvent the wheels here's two classes to help you with date and time in PHP.

### Carbon

[Carbon](https://github.com/briannesbitt/Carbon "Carbon Documentation") from [@NesbittBrian](http://twitter.com/NesbittBrian "@NesbittBrian on twitter") supercharges the `DateTime` object with many useful methods and/or properties. The class requires _PHP 5.3_

This class extends PHP internal `DateTime` class. Which means that anywhere the `DateTime` object is required you can safely substitute it with a `Carbon` instance and gain many useful getter and setter methods to truly ease `DateTime` usage.

For example, `Carbon` implements the `__toString` method and provide a simple mean to access each part of your `DateTime` object with intuitive getters properties. More information can be found on the [github homepage](https://github.com/briannesbitt/Carbon).

### Period

[Period](http://period.thephpleague.com/ "Period Documentation"), is a package that I've created and maintained as a [php league](http://thephpleague.com "the php league of extraordinary packages") package. The package contains the `Period` class which deals with time range. The class requires _PHP 5.3_

This class handles time range in a uniform and predicable way. Just like `Carbon` the class comes with many useful named constructors and can be used with `Carbon` objects. The class compares and modifies time range easily by being an immutable value object just like the `DateTimeImmutable` object.

Of course, as both classes are open sourced on Github, [Carbon](https://packagist.org/packages/nesbot/carbon "Carbon on packagist") and [Period](http://packagist.org/packages/league/period "Period on Packagist") are easily available using [composer](http://getcomposer.org "Composer website") and you are welcome to contribute to their respective code source to improve them.

## Conclusion

Dealing with date/time in PHP has evolved a great deal since PHP5 has been around and it has never been much easier. So when adding date and time capabilities in your next project, remember to use the correct class and/or to look into the open source community effort to further improve your code.
