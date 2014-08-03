---
layout: docs
title: Collection
permalink: /docs/reference/collection/
---

Collection is an PHP object that holds entities as [array object](http://www.php.net/manual/en/class.arrayobject.php). It means that you can access it as simple array with [foreach](http://www.php.net/manual/en/control-structures.foreach.php) for example.

~~~ php
$entity = new MyEntity;
$entity->name = "foor";

$collection = new UniMapper\EntityCollection("MyEntity");
$collection[] =

foreach ($collection as $entity) {

}
~~~