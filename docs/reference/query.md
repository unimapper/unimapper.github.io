---
layout: docs
title: Query
permalink: /docs/reference/query/
---

Query gives you a unique way to access your stored data with unite API, wherever they live. It communicates directly with mappers related to entity. The usage itself is very easy with fluent interface.

## Query builder
All queries are usually registered in query builder object that lives in every repository.

## Built-in queries

#### find ( `string` property1, `string` property2 .. )
Get all records as entity collection. You can use following filters:
- where()
- orWhere()
- whereAre()
- orwhereAre()
- limit()
- offset()

### findOne ( `mixed` primaryValue )
Get single unique record by priamry property value.

### insert ( `array` $data )
Insert a new record

### update ( `array` $data )
Update record.

- where()
- orWhere()
- whereAre()
- orwhereAre()

### delete ()
Delete record.

- where()
- orWhere()
- whereAre()
- orwhereAre()

## Extending queries