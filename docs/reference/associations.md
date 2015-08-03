---
layout: docs
title: Associations
permalink: /docs/reference/associations/
---

Sometimes you need to describe relation between two entities and this can be done with associations. Every association is represented by an option `m:assoc` with relation type description and its property should be target [entity]({{ site.baseurl}}/docs/reference/entity) or entity [collection]({{ site.baseurl}}/docs/reference/entity#collection), it depends on association type you choose.

## Definition
Associations are defined as [properties]({{ site.baseurl}}/docs/reference/entity#property) in entity with two required [options]({{ site.baseurl}}/docs/reference/entity#options) - `m:assoc(..)` for the association's type and `m:assoc-by(..)` for association's definition.

## Supported types

### 1:N - OneToMany
The most widely used relation states that some entity can be associated with many other entities by some foreign key.

Let's say we have a customer who has a lot of orders in our e-shop.

`@property Order[] $orders m:assoc(1:N=customerId)`

### 1:1 - OneToOne
Entity may only be associated with one other entity by some foreign key.

For example that we have a customer and his detail.

`@property CustomerDetail $detail m:assoc(1:1=customerId)`

### M:N - ManyToMany
Entity can be associated with many other entities and vice-versa. Because both entities can have many related entities a new join table will need to be created to keep track of these relations.

For example that we have employees working in multiple departments.

`@property Departments[] $departments m:assoc(M:N=employeeId|employee_department|departmentId)`

### N:1 - ManyToOne
We have an order and we want to get its customer.

`@property Customer $customer m:assoc(N:1=customerId)`

## Remote associations

You can even associate entities with cross-adapter relationship and the ORM take care of querying and merging data itself.

### Dominance

If your are using [M:N](#mn---manytomany) relationship as [remote](#remote-associations) association you may need to declare on which side join table is.
By default it's the owning side but if necessary you can change it with `M<N` in definition.

`@property Departments[] $departments m:assoc(M<N=employeeId|employee_department|departmentId)`

> Using `M>N` is the same as `M:N`.

## Getting data
After you finished entity definition you can decide whether you want to join associated entities automatically during the [query]({{ site.baseurl }}/docs/reference/query) or not.

~~~ php
namespace MyApp\Model\Repository;

class CustomerRepository extends \UniMapper\Entity
{
    public function findCustomersWithOrders()
    {
        return $this->select()
            ->associate("orders", ...)
            ->run($this->connection());
    }
}
~~~

## Filters
Filters allow you to modify associated result without any complications. Every filter must be registered globally on entity reflection and defined in property docblock as another option.

**Registration**

~~~ php
UniMapper\Reflection\Property::registerAssocFilter("sortLimit", function (UniMapper\Association\Multi $assoc, $orderBy = "ASC", $limit = 10) {
    $assoc->limit($limit)->orderBy($orderBy);
});
~~~

**Usage**

`@property Orders[] $orders m:assoc(M:N=userId|user_order|orderId) m:assoc-filter-sortLimit(DESC|10)`

> Only one filter option can be defined on every property

## Changes
Help you to manage entity or collection changes directly on property. Usage is slightly different depending on property [type]({{ site.baseurl }}/docs/reference/entity#value-type), but you can use common methods `attach`, `detach`, `remove` or `add` with both types.

### Multi
If property type is collection of entities, typically ([OneToMany](#n---onetomany) or [ManyToMany](#mn---manytomany)).

~~~ php
$user = $repository->findOne(1);
$user->orders()->attach(new Order["id" => 2]); // Order with id 2 is attached to user with id 1 so only one new record in join table will be added after save
$repository->save($user);
~~~

### Single
If property type is a single entity, typically ([ManyToOne](#n1---manytoone) or [OneToOne](#onetoone)).

~~~ php
$order = $repository->findOne(1);
$order->invoice(new Invoice)->add(); // New invoice will be created with relation to order with id 1 after save
$repository->save($order);
~~~

> Changes on property can be cleaned with FALSE argument - `$entity->property(false)`.
