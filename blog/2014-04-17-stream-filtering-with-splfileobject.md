---
title: "Stream Filtering with SplFileObject"
date: "2014-04-17"
categories: 
  - "web"
tags: 
  - "filtering"
  - "php"
  - "splfileobject"
  - "stream"
---

Since PHP4 days, the [language has been able to interact with streams](http://www.sitepoint.com/%EF%BB%BFunderstanding-streams-in-php/ "Understanding Streams in PHP"), a resource object that can be read from or written to in a linear fashion. This feature can help us applying filters function on streams while reading from or written to them. This can be interesting if you want, for instance, to compress or decompress, on the fly, a file before or after accessing it. To apply those filters, the developer must use PHP stream filtering functions `stream_filter_*` and/or the php meta wrapper `php://filter` and have access to a PHP file resource. For instance, any resource returned by `fopen` can be filtered using PHP.

```php
$path = 'path/to/my/file.txt';
$fp = fopen($path, 'r');
$filter1 = stream_filter_append($fp, 'string.toupper');
$filter2 = stream_filter_prepend($fp, 'string.rot13', STREAM_FILTER_READ);
$res = fgets($fp); //the output text is ROT13 and then uppercased
stream_filter_remove($filter2);
rewind($fp);
$res = fgets($fp); //the output text is only uppercased
```

The stream filters can be applied when reading,  writing or on both actions. They can be removed at any given time. This feature is truly powerful.

Now let's jump to today's post-PHP 5.3+ world where objects like `SplFileObject` where created to offer an OOP approach to file interaction. With the added benefit of using `Iterator` and many other goodies, being able to apply PHP stream filtering features on a `SplFileObject` as easily as on a file resource would be great but that is not currently possible. The main reason being that the `SplFileObject` class does not expose it's internal file pointer resource, so using any `stream_filter_*` is simply not possible adding stream filters to an instantiate `SplFileObject` object is not possible.

If you want to apply stream filters to a `SplFileObject` object, you are required to instantiate the object using the meta wrapper `php://filter`.

```php
$path = 'path/to/my/file.txt';
$file = new SplFileObject('php://filter/read=string.rot13|string.toupper/resource='.$path, 'r');
$file->fgets();  //the output text is ROT13 and then uppercased
```

This technique works but has several limitations, here are two that come directly in mind:

- Writing the PHP meta-wrapper can easily become a headache, if you apply several filters.
- the meta wrapper restricts the use of stream filters, as you can not append/prepend the filters after the object instantiation!!
- you can not set the stream filter mode (read and/or write) on a filter base

I understand that the `stream_filter_*` functions were first design to tackle those limitations when using a file resource. It's a bit strange that the same problem was re-introduce when `SplFileObject` was designed.

To solve theses issues PHP could expose the internal file pointer resource used by `SplFileObject`, [there's a php bug entry for that](https://bugs.php.net/bug.php?id=44392 "Bug entry to implement file pointer access to SplFileObject"). But I can imagine that exposing the file pointer resource would have some nasty consequences when using the `SplFileObject`. For instance someone could use `fclose` directly on the resource and they're maybe worse case scenario.

Another solution would be to implement `stream_filter_append` and `stream_filter_prepend` as new methods for the `SplFileObject`.

```php
$file = new SplFileObject('/path/to/my/file', 'r');
$filter1 = $file->appendStreamFilter('string.toupper');
$filter2 = $file->prependStreamFilter('string.rot13', STREAM_FILTER_READ);
stream_filter_remove($filter2);
```

This proposal would be safer to implement, IMHO.

Now don't get me wrong, this is not another attempt to go OOP with everything that exists in PHP, but I think I would benefit any codebase that relies heavily on `SplFileObject`, like my PHP CSV manipulation library [League\\Csv](http://csv.thephpleague.com/ "The CSV Manipulation library").

**Update 2014-04-29:** After thinking over this solution a bit, I think there's another solution. I think we could implement an new PHP interface called `Streamable` and `SplFileObject` would implement this interface. This interface would act like the `Traversable` interface meaning that it can not be access directly in userland but it would allow classes implementing it to work with functions like `stream_filter_append` and `stream_filter_prepend`. These functions would accept a file resource pointer and/or a Streamable class. This interface could be use on any PHP function apart from file specific function to allow `SplFileObject` to work on many other situations. It would expose internally only the object file pointer resource to the native functions.

What do you think ?

PS: I don't know the amount of code changes, it would require in the PHP source code to implement any of those proposal. But I think something must be done to allow a better use of stream filters with `SplFileObject`.
