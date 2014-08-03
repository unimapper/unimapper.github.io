---
layout: docs
title: Mapper
permalink: /docs/reference/mapper/
---

Mapper is used to translate the ORM query syntax to some database query, REST API call or something else. Once the query is correctly translated and executed, the returned data are mapped to desired [entity]({{ site.baseurl }}/docs/reference/entity/) or [collection]({{ site.baseurl }}/docs/reference/collection/).

The idea is that each of your data source should have created such a mapper.