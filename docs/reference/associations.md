---
layout: docs
title: Associations
permalink: /docs/reference/associations/
---

Sometimes you need to describe relation between two entities and this can be done with associations. Every association is represented by an option `m:assoc` with relation type description and its property should be target [entity]({{ site.baseurl}}/docs/reference/entity) or entity [collection]({{ site.baseurl}}/docs/reference/entity#collection), it depends on association type you choose.

## Supported types

### 1:N - BelongsToMany
The most widely used relation states that some entity can be associated with many other entities by some foreign key.

Let's say we have a customer who has a lot of orders in our e-shop.

`@property Order[] $orders m:assoc(1:N=customerId)`

### 1:1 - BelongsToOne
Entity may only be associated with one other entity by some foreign key.

For example that we have a customer and his detail.

`@property CustomerDetail $detail m:assoc(1:1=customerId)`

### M:N - HasMany
Entity can be associated with many other entities and vice-versa. Because both entities can have many related entities a new join table will need to be created to keep track of these relations.

For example that we have employees working in multiple departments.

`@property Departments[] $departments m:assoc(M:N=employeeId|employee_department|departmentId)`

### N:1 - HasOne
We have an order and we want to get its customer.

`@property Customer $customer m:assoc(N:1=customerId)`

## Usage
After you finished entity definition you can decide whether you want to load associated entities automatically during the query or not.

~~~ php
namespace MyApp\Model\Repository;

class CustomerRepository extends \UniMapper\Entity
{
    public function findCustomersWithOrders()
    {
        return $this->find()
            ->associate("orders", ...)
            ->execute();
    }
}
~~~

## Remote associations
> **Warning!** This feature is experimental and should be available in version 1.1.0 and higher.

You can even associate entities with different adapters across multiple data stores.