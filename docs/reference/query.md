---
layout: docs
title: Query
permalink: /docs/reference/query/
---

Query gives you a unique way to access your stored data with united API, wherever they live. It communicates directly with adapters related to entity and the usage itself is very easy with fluent interface.

## Creating queries
Queries can be created in two ways.

### Query builder

~~~ php
$queryBuilder = new UniMapper\QueryBuilder("Entity"); // Entity class, name or instance
$queryBuilder->select()->...;
~~~

### Entity

~~~ php
Entity::query()->select()->...;
~~~

## Executing queries

~~~ php
$connection = new UniMapper\Connection(new UniMapper\Mapper);
$connection->registerAdapter(...);
Entity::query()->select()->run($connection);
~~~

## Standard queries

### select ( `string` property1, `string` property2 .. )
Get all records as entity collection. You can use the following options:

- limit( `integer` )
- offset( `integer` )
- [conditions](#conditionable)
- cached( `boolean`, `array` [options]({{ site.baseurl}}/docs/reference/cache#options) )

### selectOne ( `mixed` primaryValue )
Get a single unique record by primary value.

### insert ( `array` $data )
Insert a new record

### update ( `array` $data )
Update record.

- [conditions](#conditionable)

### updateOne ( `mixed` primaryValue )
Update record by primary value.

### delete ()
Delete record.

- [conditions](#conditionable)

### deleteOne ( `mixed` primaryValue )
Delete record by primary value.

### Conditionable queries
Conditionable queries can use following methods:

- where()
- orWhere()
- whereAre()
- orwhereAre()

> Be aware of operator operator precedence, depending on your current [adapter]({{ site.baseurl }}/docs/reference/adapter/).

## Custom queries

You can even create and register your own query. This can be useful in situations
such as when you need optimized query to the database and you know that it will be
used in the same form several times in your code.

### Definition
First of all, you need to create custom query class.

~~~ php
namespace MyApp\Model\Query;

class Search extends \UniMapper\Query
{
    private $pattern;

    public function __construct(\UniMapper\Reflection\Entity $entityReflection)
    {
        parent::__construct($entityReflection);
        $this->pattern = $pattern;
    }

    protected function onExecute(\UniMapper\Connection $connection)
    {
        // Do some heavy stuff with adapter and return the result
    }
}
~~~

### Registration
Queries can be registered on [query builder](#query-builder).

~~~ php
UniMapper\QueryBuilder::registerQuery("MyApp\Model\Query\Search");
~~~

> Method name of custom query is generated from class base name, but you can change it manually by overloading method *UniMapper\Query::getName()*, but remember that resulted query name must be unique and should not collidate with [standard queries](#standard-queries).