---
layout: docs
title: Query
permalink: /docs/reference/query/
---

Query gives you a unique way to access your stored data with united API, wherever they live. It communicates directly with adapters related to entity and the usage itself is very easy with fluent interface.

## Query builder
Query builder is some kind of factory for all queries and keeps all registered [adapters]({{ site.baseurl }}/docs/reference/adapter/).

~~~ php
$queryBuilder = new UniMapper\QueryBuilder($mapper, $cache);
$queryBuilder->registerAdapter("adapterName", new Adapter);
$queryBuilder->registerAdapter(...);
~~~

## Built-in queries

### select ( `string` property1, `string` property2 .. )
Get all records as entity collection. You can use the following options:

- limit( `integer` )
- offset( `integer` )
- [conditions](#Conditions)
- cached( `boolean`, `array` [options]({{ site.baseurl}}/docs/reference/cache#options) )

### selectOne ( `mixed` primaryValue )
Get a single unique record by primary property value.

### insert ( `array` $data )
Insert a new record

### update ( `array` $data )
Update record.

- [conditions](#Conditions)

### delete ()
Delete record.

- [conditions](#Conditions)

### associate ( `mixed` $primary, `UniMapper\Association` $association )

Persists an [association]({{ site.baseeurl}}/docs/reference/associations).

### Conditions

- where()
- orWhere()
- whereAre()
- orwhereAre()

> Be aware of operator operator precedence, depending on your current [adapter]({{ site.baseurl }}/docs/reference/adapter/).

## Custom queries

You can even create and register your own query. This can be useful in situations
such as when you need optimized query to the database and you know that it will be
used in the same form several times in your code.

First of all, you need to create custom query class, which extends abstract class *UniMapper\Query\Custom*.

**Search.php**

~~~ php
namespace MyApp\Model\Query;

class Search extends \UniMapper\Query\Custom
{
    private $pattern;

    public function __construct(\UniMapper\Reflection\Entity $entityReflection, array $adapters, $pattern)
    {
        parent::__construct($entityReflection, $adapters);
        $this->pattern = $pattern;
    }

    public function onExecute(\UniMapper\Adapter $adapter)
    {
        // Do some heavy stuff with adapter and return the result
    }
}
~~~

Then you are able to register query in your [repository]({{ site.baseurl }}/docs/reference/repository/).

**OrderRepository.php**

~~~ php
namespace Model\Repository;

class OrderRepository extends \UniMapper\Repository
{
    public function search($pattern)
    {
        $this->registerCustomQuery("MyApp\Model\Query\Searcg");
        $this->query()->search($pattern)->execute();
    }
}
~~~

> Method name of custom query is generated from class base name, but you can change it manually by overloading method *getName()*, but remember that resulted query name must be unique!