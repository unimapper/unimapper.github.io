---
layout: docs
title: Entity
permalink: /docs/reference/entity/
---

Entity usually represents a unique object in your application model schema with which you are trying to faithfully capture the reality.

## Collection
Keeps entities with same type and can be accessed as [ArrayObject](http://php.net/manual/en/class.arrayobject.php).

## Properties

## Type

- **Basic** `string`, `integer`, `boolean`, `double`, `array`
- **[DateTime](http://www.php.net/manual/en/class.datetime.php)**
- **Entity** Single entity, named according to your [naming conventions]({{ site.baseurl }}/docs/reference/naming-conventions/)
- **Entity\[\]** Entity [collection](#collection) stored inside the `UniMapper\EntityCollection` class

## Adapter

/**
 * @adapter YourAdapterName(user_table)
 */
class User extends \UniMapper\Entity
{

}
~~~

## Options

You can pass some additional informations via options. Each option is prefixed with `m:` and consists of key name and values.
You can choose from some built-in options.

### Primary
Represents some kind of *foreign key* similar to relational database and every entity can be identified by it.
Usually some `id` column in your database for example.

~~~ php
/**
 * @property integer $id m:primary
 */
class User extends \UniMapper\Entity
{}
~~~

### Mapping
You can tell entity how to map your data with `m:map`.

- `name` - Describes alternative column name in database for example.
- `filter` - You can tell how to map out/in data.

~~~ php
/**
 * @property array $list m:map-by(json_data) m:map-filter(jsonToArray|arrayToJson)
 */
class User extends \UniMapper\Entity
{
    public static function jsonToArray($value)
    {
        return json_decode($value);
    }

    public static function arrayToJson(array $value)
    {
        return json_encode($value);
    }
}
~~~

### Computed
A kind of virtual property, mostly dependent on other real properties so it is readonly and can not be set directly. It can be helpful in situations like price computing for example.

~~~ php
/**
 * @property double $price
 */
class Product extends \UniMapper\Entity
{}

/**
 * @property Product[] $products
 * @property double    $price    m:computed
 */
class Order extends \UniMapper\Entity
{
    protected function computePrice()
    {
    	$price = 0;
    	foreach ($this->products as $product) {
    	    $price += $product->price;
    	}
        return $price;
    }
}

$orderRepository = new OrderRepository;
$productRepository = new ProductRepository;

$order = $orderRepository->createEntity();
$product1 = $productRepository->createEntity();
$product1->price = 5.0;
$order->products[] = $product1;

echo $order->price; // Will be 5.0

$product2 = $productRepository->createEntity();
$product2->price = 10.0;
$order->products[] = $product2;

echo $order->price; // Will be 15.0
~~~

> Computed property can not be mixed with other options.

### Associations
See [this article]({{ site.baseurl }}/docs/reference/associations).