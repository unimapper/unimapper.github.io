---
layout: docs
title: Cache
permalink: /docs/reference/cache/
---

## Implementation
Library does not provide any built-in cache, but there is an interface `UniMapper\Cache\ICache` you can use with following predefined methods:

- load ( `mixed` key )
- save ( `mixed` key, `mixed` data, `array` [options](#options) ) = [] )

> [Options](#options) should be implemented in `save()` method.

## Usage
You do not anything special, just register your cache on every repository and library takes care about reflection and queries caching automatically.

~~~php
$repository = new SomeRepository;
$repository->setCache(/* Your cache instance */);
~~~

## Options
Sometimes you need to tell how long is your data in cache valid or add some common tag, file dependencies, whatever else.
For these purposes every cache keeps some predefined unique constants with these options.

For example we have a query that should be cached and we want to add some tags and time expiration.

**SomeRepository.php**

~~~php
$this->query()
    ->select()
    ->cached(true, [
        UniMapper\Cache\ICache::TAGS => ["tag1", "tag2"],
        UniMapper\Cache\ICache::EXPIRE => ["20 minutes"]
    ])
    ->execute();
~~~