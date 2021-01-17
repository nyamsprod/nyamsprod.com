---
layout: post
title: "League CSV now supports streams"
date: "2017-01-25"
categories: 
  - "web"
tags: 
  - "csv"
  - "php"
  - "stream"
  - "the-php-league"
---

One of the long requested feature to be added to the CSV was stream supports. Starting with [League\\Csv 8.2](https://github.com/thephpleague/csv/blob/master/CHANGELOG.md#820---2017-01-25), the wait is over, you'll be able to manipulate CSV objects created from a resource stream. As an example you can now do this

{% gist e02c92af21ec8097b6c7f465a9b9385f stream-reader.php %}

Because your CSV object is created using a resource stream you will not be able to use [the CSV stream filter capabilities](http://csv.thephpleague.com/filtering/) but since you are already using a resource stream, it does not matter because you can directly use PHP's stream filter capabilities like shown below.

{% gist e02c92af21ec8097b6c7f465a9b9385f stream-writer.php %}

As you can see supporting streams enables more interactions with CSV documents while still using a familiar API.

### Final note

The [League CSV](https://github.com/thephpleague/csv) is an open source project with a MIT License so contributions are more than welcome and will be fully credited. These contributions can be anything from reporting an issue, requesting or adding missing features or simply improving or correcting some typo on the documentation website.
