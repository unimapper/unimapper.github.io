---
layout: docs
title: Repository
permalink: /docs/reference/repository/
---

Repository makes data accessing easy in an OOP friendly way. It takes care about [entities]({{ site.baseurl }}/docs/reference/entity), their persistance and loading. An additional advantage of repositories is that your model layer can be easily mocked in your unit tests.

### Default methods

#### count ( `array` $filter )

#### delete ( `UniMapper\Entity` $entity )

#### find ( `array` $filter, `array` $orderBy, `int` $limit, `int` $offset, `array` $associate )

#### findOne ( `mixed` $primary )
Returns a single entity by its unique primary value.

#### findPrimaries( `array` $primaryValues)

#### insert ( `UniMapper\Entity` $entity )
Insert data from entity to your storage as a new record. Primary value is ignored but returned.

#### save ( `UniMapper\Entity` $entity )
Persists given entity. If primary value set on entity it calls insert, if not then update.

#### update ( `UniMapper\Entity` $entity )