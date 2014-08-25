---
layout: docs
title: Get involved
permalink: /docs/extensions/get-involved/
---

> You can share your extensions [here](https://github.com/unimapper/unimapper.github.io/issues/new).

If there is a situation that you have a data source that is not covered by an extension of cummunity,
it is possible to write your own. The library is designed to make it as easy as possible at least the effort.

## Custom adapter
Usually, you just write your own adapter, which should implement all methods listed in the interface.
The contents of these methods should concern itself only retrieving data from a data source, nothing more.

## Custom mapping
However, there may be situations where data that the adapter receives from queries or data source,
still need a little intervention during mapping, and therefore each adapter can implement its own mapping descendant.
