---
layout: docs
title: Connections
permalink: /docs/get-started/connections/
prev_section: /get-started/entities
next_section: /get-started/repositories
---

We know how and where are entities stored and now we need to define connection between our application and storages we have. For this purpose we use [adapters]({{ site.baseurl }}/docs/reference/adapter).

And there are two adapters in our application.

- [Dibi]({{ site.baseurl }}/docs/extensions/browse/#dibi) for orders and customers
- [Mongo]({{ site.baseurl }}/docs/extensions/browse/#mongo) for invoices

**./index.php**

~~~ php
$dibiConnection = new \DibiConnection([
    "driver" => "mysql",
    "host" => "localhost",
    "database" => "get_started",
    "user" => "root",
    "lazy" => true
]);
$dibiAdapter = new \UniMapper\Dibi\Adapter(
    "Dibi",
    $dibiConnection
);

$mongoAdapter = new UniMapper\Mongo\Adapter("Mongo", ["database" => "get_started"]);
~~~

> Adapter name should match with its definition in entity!