---
layout: post
title: "Tutorial : How to cache a resource using PHP"
date: "2014-02-10"
categories: 
  - "web"
tags: 
  - "browser"
  - "cache"
  - "http-headers"
  - "php"
  - "scripting"
  - "tutorial"
---

In this tutorial I'll show you how to add a smart cache system to a resource using PHP. This tutorial can be adapted to any scripting language as long as you adapt the functions too, since the logic will remain the same.

## Starting point

The tutorial uses a very basic script:

- A user sends some informations to a server;
- Using this information, a script generate some data;
- The data is then returned to the client encoded in Json format;

So we have 3 functions:

- `filterInput` that filter incoming parameters from the client request;
- `fetchData` that fetch the data using the developer business logic;
- `outputEscapedJson` that encode the data to be Json outputted correctly;

For the purpose of this tutorial we will assume that those functions have been tested and they work :) !

### PHP default behavior

So the script is really as simple as the code below:

```php
<?php
$params = filterInput($_GET);
$data = fetchData($params);
echo outputEscapedJson($data);
```

This code will work, but you have to keep in mind that PHP made some assumptions when generating the response:

- PHP sent a `HTTP Status Code` equals to 200 meaning that the client request was OK;
- PHP sent a `Content-Type` header specifying that your where delivering HTML content. Your information will be understood by the client (ie: the browser) as being HTML rather than Json;

To fix the second issue we will take control of the HTTP Response produced by PHP.

### Introducing PHP `header` function

To do so, we will use the `header` function from PHP which manipulate HTTP response headers and status code. Using this function you can virtually manipulate any HTTP header (including cookies). So let's improve our code:

```php
<?php
$params = filterInput($_GET);
$data = fetchData($params);
$json = outputEscapedJson($data);

//final Response header
header("Content-Type: application/json; charset=utf-8");
header("Content-Length: ".strlen($json));
die($json);
```

We've included 2 headers:

- the `Content-Type` that indicate that we are sending UTF-8 generated Json;
- the `Content-Length` that indicate the size of the content.;

By default when everything is OK, PHP sends a HTTP Status Code equals to 200. So we don't need to explicitly change this status.

Now that the browser knows that the response content type will be Json, let's cache our resource.

## Adding Server Side Cache

There are many ways to implement a cache on the server but for simplicity I'll implement a file based cache system since PHP provides built-in functions to easily implement this type of cache. But keep in mind that whatever cache system you choose the logic will remain the same:

- We need to check if the result is already present in the cache;
- If the answer is yes we will use the cache data;
- Otherwise, we generate the result and save it in the cache for future use;

To do so we will add a new function:

- `fetchCacheFilePath` which returns the cache file attached to the user `$params`.

```php
<?php
$params = filterInput($_GET);
$cache = fetchCacheFilePath($params);

//Server Cache
if (! file_exists($cache)) {
    $data = fetchData($params);
    $json = outputEscapedJson($data);
    file_put_contents($cache, $json);
}

header("Content-Type: application/json; charset=utf-8");
header("Content-Length: ".filesize($cache));
readfile($cache);
```

Notice how we have change the `Content-Length` header, now the information is taken directly from the file.

Adding a cache system has also introduced several problems, what happens when:

- the cache can not saved the data (ie: the file can not be created by `file_put_contents`);
- the cache data is corrupted (ie: the file is readable but for unknown reason `readile` does not work);
- the data is present but can not be read (ie: the file exists but is not be readable by your webserver);

Luckily for us there are HTTP Status Code for that. So let's introduce them:

- The 500 status code happens when an unexpected condition occurs, so if you can't save the data or can't output it, we will use this status code;
- The 403 Status code means that the server understood my request but is refusing (in our cases not able to) fullfil the request because the resource is not readable;

So the code becomes:

```php
<?php
$params = filterInput($_GET);
$cache = fetchCacheFilePath($params);

//Server Cache
if (! file_exists($cache)) {
    $data = fetchData($params);
    $json = outputEscapedJson($data);
    //The cache can not be generated
    if (! file_put_contents($cache, $json)) {
        header("HTTP/1.1 500 Internal Server Error");
        die;
    }
}

//Resource accessibility
if (! is_readable($cache)) {
    header("HTTP/1.1 403 Forbidden");
    die;
}

//Final response header
header("Content-Type: application/json; charset=utf-8");
header("Content-Length: ".filesize($cache));
if (! @readfile($cache)) {
    header("HTTP/1.1 500 Internal Server Error");
    header("Content-Length: 0");
    die;
}
```

**Of note:**

- For the last 500 status code, I'm adding the `Content-Length` header equal to `0` to replace the previously declare header;
- To be totally complete I'll advise the developer to add an event dispatcher system to this process so that when errors like those documented here happen he(she) is informed by mail for example;

This cache works but it has a problem, it never expires!!

This could be problematic, if what you store can changed in time, we need to add expiration logic so that our cache remains "fresh". Let do that by moving the `file_exists` function into a more appropriate function `isCacheValid`.

This will result in the code below:

```php
<?php
date_default_timezone_set('UTC');

/**
* Check to see if the cache is still valid
*
* @param string $cache cache file path
* @param string $ttl a string representing the relative formats supported by the parser used for strtotime() and DateTime.
*
* @return boolean
*/
function isCacheValid($cache, $ttl)
{
    if (! file_exists($cache)) {
        return false;
    }
    //check if the file needs to be refreshed or not ?
    $last_modified = new DateTime('@'.filemtime($cache));
    $expire = new DateTime('-'.$ttl, new DateTimezone('UTC')));
    return $last_modified > $expire;
}

$ttl = '1 DAY'; //duration of the server cache
$params = filterInput($_GET);
$cache = fetchCacheFilePath($params);
//Smarter Server Cache
if (! isCacheValid($cache, $ttl)) {
    $data = fetchData($params);
    $json = outputEscapedJson($data);
    if (! file_put_contents($cache, $json)) {
        header("HTTP/1.1 500 Internal Server Error");
        die;
    }
    //because the file might have been regenerated
    clearstatcache(true, $cache);
}

if (! is_readable($cache)) {
    header("HTTP/1.1 403 Forbidden");
    die;
}

header("Content-Type: application/json; charset=utf-8");
header("Content-Length: ".filesize($cache));
if (! @readfile($cache)) {
    header("HTTP/1.1 500 Internal Server Error");
    header("Content-Length: 0");
    die;
}
```

**Of note:**

- Since we are refreshing according to time it is best practice to indicate your current Timezone with `date_default_timezone_set`. To make sure that the DateTime objects are all compared on the same settings;
- We've added the `clearstatcache` function because the cache file can be regenerated even if it already existed;

Server side speaking, your cache is finished and all is well. But what if you could improve even more your cache logic using your client's application cache features. This would make your script even more awesome, let's do that!!

## Adding Client Side Cache on a HTTP compliant applications (ie: a browser)

If implemented correctly this cache will reduce your application bandwidth by caching the resource on the client software.

To use the HTTP protocol for caching you need to provide 2 types of rules to the client:

- a validation rule to validate the content you wish to cache;
- a refresh rules to indicate when you wish the resource to be refresh;

The HTTP protocol provides several mechanisms but for this tutorial I'll use:

- the last modified header as a validator information;
- the expires headers as a refresh information;

Once again the strategy you choose depends on how and what you wish to save. But whatever the chosen solution is, the logic remains the same.

- The client issue a first request;
- The server sends to the client a validator and a refresh information header;
- The client issue a second request by adding a new header request for the resource;
- Depending on the presence and on the value of the new header the server will tell the browser to use its cache or will send a updated version of the resource;

Let's update once again our code :) .

```php
<?php
date_default_timezone_set('UTC');

function isCacheValid($cache, $ttl)
{
    if (! file_exists($cache)) {
        return false;
    }
    $last_modified = new DateTime('@'.filemtime($cache));
    $expire = new DateTime('-'.$ttl, new DateTimezone('UTC')));
    return $last_modified > $expire;
}

$ttl = '1 DAY';
$params = filterInput($_GET);
$cache = fetchCacheFilePath($params);
if (! isCacheValid($cache, $ttl)) {
    $data = fetchData($params);
    $json = outputEscapedJson($data);
    if (! file_put_contents($cache, $json)) {
        header("HTTP/1.1 500 Internal Server Error");
        die;
    }
    clearstatcache(true, $cache);
}

if (! is_readable($cache)) {
    header("HTTP/1.1 403 Forbidden");
    die;
}

//HTTP Cache Verification
$last_modified = new DateTime('@'.filemtime($cache));
$expires = clone $last_modified;
$expires->modify('+'.$ttl);
header("Last-Modified: ".$last_modified->format(DATE_RFC1123));
header("Expires: ".$expires->format(DATE_RFC1123));
if (
    isset($_SERVER['HTTP_IF_MODIFIED_SINCE'])
    && $last_modified <= new DateTime($_SERVER['HTTP_IF_MODIFIED_SINCE'])
) {
    header("HTTP/1.1 304 Not Modified");
    die;
}

header("Content-Type: application/json; charset=utf-8");
header("Content-Length: ".filesize($cache));
if (! @readfile($cache)) {
    header("HTTP/1.1 500 Internal Server Error");
    header("Content-Length: 0");
    die;
}
```

The crucial parts added are:

- the `Last-Modified` and the `Expires` headers with content according the HTTP headers protocols.
- the `$_SERVER['HTTP_IF_MODIFIED_SINCE']` used to check whether the resource is changed or not.

If the resource has not changed we issue a **304 HTTP Status Code** which means that the browser must use its own cache.

**Of Note:**

- for simplicity I'm using the same cache parameter for the server **and** the client but nothing prevents you for having 2 different values for both cache it really depends on you business logic;
- Alternatively you can use the `Etag` header as a validator rules and the `Cache-control` header as a refresh rules to achieve the same browser cache. The only difference is that when you use the `Etag` header you must validate you resource against the `$_SERVER['IF_NONE_MATCH']` value if it exists;

Following this simple tutorial you have learn how to cache a resource, server side and client side in PHP. But above all, now you should understand that knowing and understanding HTTP protocols is a very important asset for anyone who wants to master how the web works.
