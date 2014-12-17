---
layout: docs
title: Entities
permalink: /docs/get-started/entities/
prev_section: /get-started/create-app
next_section: /get-started/connections
---

First of all we need to describe how the data is stored. This can be done with [entities]({{ site.baseurl }}/docs/reference/entity).

And we have 3 entities in this case.

## Customer

Represents customer information from MySQL table `customers`. Notice that there is
a [computed property]({{ site.baseeurl}}/docs/reference/entity#computed) `fullName`
that contains customer's full name composed of name and surname and
[association]({{ site.baseeurl}}/docs/reference/associations#n---onetomany)
`orders` that joins associated orders as [entity collection]({{ site.baseeurl}}/docs/reference/entity#collection) by column `customer_id` from MySQL table `orders`.

**./Model/Entity/Customer.php**

~~~ php
namespace GetStarted\Model\Entity

/**
 * @adapter Dibi(customer)
 *
 * @property integer  $id       m:primary
 * @property string   $name
 * @property string   $surname
 * @property string   $fullName m:computed
 * @property string   $email
 * @property Order[]  $orders   m:assoc(1:N) m:assoc-by(customer_id)
 */
class Customer extends \UniMapper\Entity
{

    protected function computeFullName()
    {
        return $this->name . " " . $this->surname;
    }

};
~~~

## Invoice

**./Model/Entity/Invoice.php**

~~~ php
namespace GetStarted\Model\Entity;

/**
 * @adapter Mongo(invoice)
 *
 * @property string  $id     m:primary m:map-by(_id)
 * @property Order[] $orders m:assoc(1:N) m:assoc-by(invoice_id)
 */
class Invoice extends \UniMapper\Entity
{

}
~~~

## Order

**./Model/Entity/Order.php**

~~~ php
namespace GetStarted\Model\Entity;

/**
 * @adapter Dibi(order)
 *
 * @property integer  $id       m:primary
 * @property Customer $customer m:assoc(N:1) m:assoc-by(customer_id)
 * @property DateTime $time
 * @property string   $status   m:enum(self::STATUS_*)
 * @property Invoice  $invoice  m:assoc(N:1) m:assoc-by(invoice_id)
 */
class Order extends \UniMapper\Entity
{

    const STATUS_NEW = 0,
          STATUS_FINISHED = 1;

}
~~~

> And do not forget to require all these files in **index.php** too!