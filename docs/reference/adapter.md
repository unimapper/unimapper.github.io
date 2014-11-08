---
layout: docs
title: Adapter
permalink: /docs/reference/adapter/
---

Adapter is used to translate [query]({{ site.baseurl }}/docs/reference/query/) syntax to some database query, REST API call or something else. Once the query is correctly translated and executed, the returned data are mapped to desired [entity]({{ site.baseurl }}/docs/reference/entity/) or [collection]({{ site.baseurl }}/docs/reference/collection/).

The idea is that each of your data source should have created such an adapter.

> Every adapter have its own requirements, but there is a name, which must be unique and should corespond with `@adapter` definition in [entity]({{ site.baseurl }}/docs/reference/entity#adapter).

## Writing adapters
You must implement all methods listed in the interface and the contents of these methods should concern itself only retrieving data from a data source, nothing more.

## Custom mapping
There may be situations where data that the adapter receives from queries or data source, still need a little intervention during mapping, and therefore each adapter can implement its own mapping descendant.