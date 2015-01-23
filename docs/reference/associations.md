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

`@property Departments[] $departments m:assoc(M<N=employeeId|employee_department|departmentId)`.

> Using `M>N` is the same as `M:N`.

## Getting data
After you finished entity definition you can decide whether you want to load associated entities automatically during the query or not.

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

## Changes

Changes help you to manage associated entities.

~~~ php
$invoice = $invoiceRepo->createEntity();
$invoice->orders()->attach($orderRepo->findOne(1));

$invoiceRepo->save($invoice); // New invoice will be created with relation to order with id 1
~~~

### Multi
If associations's property type is collection of entities (OneToMany or ManyToMany).

- add ( `UniMapper\Entity` $entity )
- remove ( `UniMapper\Entity` $entity )
- attach ( `UniMapper\Entity` $entity )
- detach ( `UniMapper\Entity` $entity )

### Single
If associations's property type is single entity (ManyToOne or OneToOne).