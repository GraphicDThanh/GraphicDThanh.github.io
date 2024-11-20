---
title: "Asking to know basic about HTTP Cache"
excerpt_separator: <!--more-->
categories:
  - Network
tags:
  - network
  - dns
---

![](/assets/images/2023/03/2023-03-tim-hieu-ve-dns-cover.webp)

> The fastest HTTP request is the one not made. _ Unknown

Today, we learn about HTTP Cache – the key of fastest HTTP request by some questions

## What is Caching?
Caching is a technique that stores a copy of a given resource and serves it back when requested(_ from MDN)                      

## What is cache concept?​
```python
if "exist" in cache:               #  cache hit
    // use data from cache
else:                              #  cache miss
    // calculate data then set to cache
```

## What is HTTP Caching?
HTTP Caching is the way Cache apply on HTTP protocol(HTTP/1.1, HTTP/1.2)

## Why do we cache?
Because we all love fast website and Cache is a hero on improve performance

## What is basic cache mechanisms in HTTP cache?
The basic cache mechanisms is ensuring that each server response provides the correct HTTP header directives(Cache-Control) to instruct the browser on when and for how long the browser can cache the response

## How many kinds of HTTP cache?
There are 3 kinds of HTTP cache:

♠ No cache

♠ Shared cache

♠ Local(private) cache

## How many kinds of cache request directives?​
There are many kind of cache request directives. Base on using, there are 2 groups using them “used by the client in HTTP request” and “used by the server in HTTP response”

⇒ use both group: no-cache, no-store, max-age, no-transform

⇒ client side – HTTP request: max-stale, min-fresh, only-if-cached

⇒ server side – HTTP response: public, private, must-revalidate, proxy-revalidate, x-manage

Below image showing us the way to choice request directives:

http-cache-decision-tree
source: developer.google.com

## How do you get the best of both worlds: client-side caching and quick updates?​
Best practice is no-cache on html file, using unique URLs for css, js files

source: developer.google.com

Please see how client-side caching and on-demand updates:

source: MDN dev docs

## What is "bộ ba siêu đẳng" for HTTP Caching handling?​
ETag + Cache Control + unique URLs helps us deliver the best of all worlds:

⇒ long-live expiration times

⇒ control over where the response can be cached

⇒ on-demand update

## How to define target should use specific cache?​
(For ex: Cache for desktop user should not be apply for mobile user)

We can define different content based on different request header(Vary) such as cookies, language, user-agent

## How's about Cache policy?
There’s no one best cache policy, depending on your application(requirements, traffic, data, …) you must define and config your pre-source setting and your “cache hierarchy”

There are some tips, check list when working on Cache:

⇒ Use consistent URLs

⇒ Ensure server provide a validate token (ETag)

⇒ Identify which resource should cache intermediaries

⇒ Determine cache life time for each resource

⇒ Determine cache hierarchy

⇒ Minimize churn by separate resources

We just go around some basic questions about HTTP Cache. If you have more question on this, please put it to comment

In next article, we will learn more about Django Cache systems, how we apply these knowledges to Django application to improve performance of app and api

Some reference links:

   – [[Google Dev Doc] HTTP Caching](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching)

   – [[MDN web docs] HTTP Caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)