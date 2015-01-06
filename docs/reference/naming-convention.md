---
layout: docs
title: Naming convention
permalink: /docs/reference/naming-convention/
---

Naming conventions are neccesary if you want to have your [entity]({{ site.baseurl }}/docs/reference/entity/) or [repository]({{ site.baseurl }}/docs/reference/repository/) classes under the certain [namespace](http://www.php.net/manual/en/language.namespaces.php).
Just define your mask with `*`.

**Example**

~~~ php
use UniMapper\NamingConventions as UNC;

UNC::setMask("YourApp\Model\Entity\*", UNC::ENTITY_MASK); // Default is 'Model\Entity\*'
UNC::setMask("YourApp\Model\Repository\*Repository", UNC::REPOSITORY_MASK); // Default is 'Model\Repository\*Repository'
~~~

> All conventions must be set before you start using ORM.