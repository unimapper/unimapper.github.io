---
layout: docs
title: Naming convention
permalink: /docs/reference/naming-convention/
---

Naming conventions are neccesary if your want to have your [entities]({{ site.baseurl }}/docs/reference/entity/) or [repositories]({{ site.baseurl }}/docs/reference/repository/) classes under the certain [namespace](http://www.php.net/manual/en/language.namespaces.php).
Just define your mask with `*`.

**Example:**

~~~ php
use UniMapper\NamingConventions as UNC;

UNC::$entityMask = "YourApp\Model\Entity\*"; // Default is 'Model\Entity\*'
UNC::$repositoryMask = "YourApp\Model\Repository\*Repository"; // Default is 'Model\Repository\*Repository'
~~~

> These settings must be set before you start the library.