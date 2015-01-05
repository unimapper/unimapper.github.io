---
layout: docs
title: Adapter
permalink: /docs/reference/adapter/
---

Adapter is the middleman (or middlelady) between the app and the database, REST API or whatever else. The idea is that each of your data storage should have created such an adapter and every adpater's instance keeps a unique connection to it.

> Every adapter should have its own requirements obviously passed in constructor, but all of them must be registered under a unique name, which must should corespond with `@adapter` definition in [entities]({{ site.baseurl }}/docs/reference/entity#adapter).

## Writing adapters
You must implement all methods listed in the interface and the contents of these methods should concern itself only retrieving data from a data source, nothing more.

## Custom mapping
There may be situations where data that the adapter receives from queries or data source, still need a little intervention during mapping, and therefore each adapter can implement its own mapping descendant.