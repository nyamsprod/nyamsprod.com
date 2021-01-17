---
layout: post
title: "Getting the first day of the previous month in PHP"
date: "2014-03-31"
categories: 
  - "web"
tags: 
  - "date"
  - "datetime"
  - "php"
---

Today a colleague of mine came to me with a simple question.

> How to get the first day of the previous month in PHP ?

My colleague was using the following code:

```php
<?php
echo date('Y-m-01', strtotime('-1 MONTH')), PHP_EOL;
```

But the code would not work and would instead return the first day of the current month. [This behavior is documented in the PHP documentation](http://be2.php.net/manual/en/datetime.add.php#example-2322 "beware when adding month in PHP") so after some quick thinking here's the code we ended up using:

```php
<?php
echo  date('Y-m-d', strtotime(date('Y-m-01').' -1 MONTH')), PHP_EOL;
```

We first detect the first day of the current month and then we substract 1 month.

Now to be completely honest, this code sucks but we are still going to use it because it will run on any PHP version. But If you are using a version of PHP>=5.3 you should know that the parsing algorithm has been improved. So next time you really need this information use the following code:

```php
<?php
date_default_timezone_set('UTC'); //should be set in your script or in your php.ini
$date = new DateTime('FIRST DAY OF PREVIOUS MONTH');
echo $date->format('Y-m-d'), PHP_EOL;
```
