---
title: "Using Doctrine Collections  to improve CSV filtering"
date: "2018-08-15"
categories: 
  - "web"
tags: 
  - "array"
  - "collections"
  - "csv"
  - "doctrine"
  - "filtering"
  - "iterator"
  - "php"
  - "query"
  - "stream"
---

I'm happy to announce the release of [League CSV - Doctrine Collection Bridge](https://github.com/bakame-php/csv-doctrine-collections-bridge) version 1.0.0. The new package under the bakame namespace is an extension to [League\\Csv](https://csv.thephpleague.com/) which takes advantage of Doctrine Collections features to better manipulate CSV documents.

### CSV Filtering

When working with imported CSV documents it always comes down to filtering and querying data from the document to apply some business logic to them. One of the often suggested method is to import the CSV document data into a RBMS and then use its filtering capabilities to process the data. While this might be tempting it also means wasting  times in thinking about tables structure and resource availability  while often you only want to consume your data and move on to other tasks.

### League Csv Statement

For that reason I always prefer using the `League\Csv\Statement` class. The class uses closures and callables to filter the CSV document as shown below:

\[gist id="12e6d01da00176ce00a70f9288561bc9" file="csv-filtering.php"\]

### Doctrine Collection Criteria

While using the `League\Csv\Statement` is straightforward, building the correct closure/callable for a given filtering can become a daunting task. Luckily for us, the people behind the Doctrine project have long since resolve this issue with their powerful expression API by introducing the `Doctrine\Common\Collections\Criteria` class.

Using the `Criteria` class you can rewrite my previous example as follow:

\[gist id="12e6d01da00176ce00a70f9288561bc9" file="criteria-example.php"\]

Which may sound a bit overcomplicated for a simple query but ease debugging and maintenance as filtering requirements become more complex. [The expression API](https://www.doctrine-project.org/projects/doctrine-collections/en/latest/expressions.html#expressions) is similar to SQL statements so they are easy to understand and use.

### From Doctrine Criteria to Csv Statement

This package enables converting any `Doctrine\Common\Collections\Criteria` object into a `League\Csv\Statement` object allowing using Doctrine Expression API on any CSV document.

\[gist id="12e6d01da00176ce00a70f9288561bc9" file="criteria-converted.php"\]

### From  a Csv Reader to a Doctrine Collection

But that's not all the package also comes bundle with an implementation of Doctrine Collection, the `Bakame\Csv\Extension\RecordCollection` that can turn any `League\Csv\Reader` or `League\Csv\ResultSet` into a Doctrine Collection.

\[gist id="12e6d01da00176ce00a70f9288561bc9" file="record-collection.php"\]

### Final notes

Depending on your CSV size you may prefer using the `Bakame\Csv\Extension\RecordCollection` class instead of the `League\Csv\ResultSet` as the latter uses PHP Iterator and streaming capabilities to reduce memory usage.

### Last but not least

The [League CSV - Doctrine Collection Bridge](https://github.com/bakame-php/csv-doctrine-collections-bridge) is an open source project with a MIT License so contributions are more than welcome and will be fully credited. These contributions can be anything from reporting an issue, requesting or adding missing features or simply improving or correcting some typo on the documentation website.
