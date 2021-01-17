---
layout: post
title: "Q&A: Enforcing enclosure with League\Csv"
date: "2015-08-26"
categories: 
  - "web"
tags: 
  - "csv"
  - "enclosure"
  - "filter"
  - "fputcsv"
  - "php"
  - "stream"
---

It is common knowledge that PHP's `fputcsv` function [does not allow enforcing the enclosure on every field](http://stackoverflow.com/questions/2489553/forcing-fputcsv-to-use-enclosure-for-all-fields).  Using  League CSV and PHP stream filter features  let me show you how to do so step by step.

### 1 - Install league csv

if you don't already have it around, you can install the latest stable version using `Composer`.

\[prism field=snippet\_enclosure\_install\_league\_csv language=javascript\]

### 2 - Choose a sequence to enforce the presence of the enclosure character

According to [PHP fputcsv source code](https://github.com/php/php-src/blob/master/ext/standard/file.c#L1879) the enclosure is added only under the following circumstances:

- one of the CSV control character is present in the field (delimiter, enclosure or escape character);
- the newline or the tab character are present in the field `\n`, `\r`, `\t`
- the space character is present

In my example I'm going to use the tab character and another _exotic_ character.

{% gist 6cb02e92e4820093b782 sequence.php %}

### 3 - Set up you CSV

{% gist 6cb02e92e4820093b782 writer-setup.php %}

### 4 - Enforce the sequence on every CSV field

Using [the formatting capabilities of the Writer object](http://csv.thephpleague.com/inserting/#row-formatting) you can easily add the sequence to each CSV field

{% gist 6cb02e92e4820093b782 formatter.php %}

Every time you add a row with the Writer class prior from being added the row will be prepended with the `$sequence` sequence.

### 5 - Create a stream filter

This is were _the magic happens._ One of the overlooked feature of the package is that [it can use stream filters to enhance CSV alteration](http://csv.thephpleague.com/filtering/). **A stream filter can modify your CSV content after PHP's `fputcsv` has formatted your row but before the content is actually save to the file**.

I've created a stream filter class by extending PHP's `php_user_filter` class. You can view the source code via the following gist .

{% gist 6cb02e92e4820093b782 RemoveSequence.php %}

The main code is in the `RemoveSequence::filter` method. What this code does is basically removing the added sequence that enforces the enclosure character from the CSV content prior to it being saved to the file but after PHP `fputcsv`.

### 6 - Attach the stream filter to the Writer object

{% gist 6cb02e92e4820093b782 register.php %}

- `registerStreamFilter`: is a static method to ease registering the class as a possible stream filter;
- `createFilterName`: is a static method to ease generating the stream filtername to attach to the Writer object according to the CSV control characters and the added sequence;

To apply a valid and efficient filter you are required to choose a sequence which is:

- unique;
- does not contain any newline character;
- does not contain any space or null byte character;
- does not contain an already used CSV control character;

This is the reason why I choose the tab character. The extra character is added in case your data already contains a tab character to make your added sequence truly unique. The enforce sequence must be unique and as small as possible too.

### 7 - Create you CSV

Now that all the pieces are in place let's create the CSV row

{% gist 6cb02e92e4820093b782 write.php %}

### Conclusion

Et voila! You've created a CSV with enforced enclosure on everyone of its field. Let's recap it all:

{% gist 6cb02e92e4820093b782 script.php %}

### Footnotes

Of note, In the recap script I've added [an extra validation step](http://csv.thephpleague.com/inserting/#row-validation) to illustrate another feature of the `League\Csv\Writer` object which is to validate a row prior to its insertion according to your own rules. If a cell is invalid a `League\Csv\Exception\InvalidRowException` expection is thrown.

As you may have guess it, the formatting and the validation steps are optional. If you already have formatted and validated your data prior to the insertion, you don't need them. Conversely,  the addition of the sequence before insertion and its subsequent subtraction using a stream filter is required.

Registering the stream filter can be done in the script or in the bootstrap script of your application. You should not register the stream filter prior to each usage, but your are required to attach it to the `League\Csv\Writer` object in order to use it.

This technique works even without the league CSV library as long as you are able to manipulate your CSV as a stream on insertion.

In case of the League CSV there are some trade-offs when using this technique:

- Its usage is limited by how `SplFileObject` supports stream filters;
- `League\Csv\Writer` insertion speed is slowed down because of  the extra steps you are adding;

### Last but not least

The League\\Csv is an open source project with a MIT License so contributions are more than welcome and will be fully credited.  These contributions can be anything from reporting an issue, requesting or adding missing features or simply improving or correcting some typo on the documentation website.
