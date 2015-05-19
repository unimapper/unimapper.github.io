---
layout: docs
title: Entity
permalink: /docs/reference/entity/
---

Entity usually represents a unique object in your application model schema with which you are trying to faithfully capture the reality. Every entity must have a common ancestor `UniMapper\Entity` and all custom definitions you write in [PHPDoc](http://en.wikipedia.org/wiki/PHPDoc) comments of every single entity class in you app.

## Collection
Entities can be grouped in collection that helps you keep its class type and you can access them as simple [ArrayObject](http://php.net/manual/en/class.arrayobject.php).

~~~ php
$collection = new UniMapper\EntityCollection("Entity");
$collection[] = new Entity;

foreach ($collection as $entity) {
    echo $entity->id;
}
~~~

## Adapter
[Adapter]({{ site.baseurl }}/docs/reference/adapter/) is tied with entity by name you provided in adapter registration on query builder and target resource (eg. table name) as required parameter.

~~~ php
/**
 * @adapter YourAdapterName(user_table)
 */
class User extends \UniMapper\Entity
{}
~~~

## Property
Properties consist of [access definition](#access-definition), [value type](#value-type) and [options](#options).

### Access definition

- `@property` you can write and read.
- `@property-read` readonly access.

### Value type

- **Basic** `string`, `integer`, `boolean`, `double`, `array`
- **[DateTime](http://www.php.net/manual/en/class.datetime.php)**
- **Entity** Single entity, named according to your [naming conventions]({{ site.baseurl }}/docs/reference/naming-conventions/)
- **Entity\[\]** [entity collection](#collection)
- **Date** accepts [DateTime](http://www.php.net/manual/en/class.datetime.php) object but date format given after entity serialization. Output format can be changed like via

~~~ php
UniMapper\Entity::$dateFormat = "Y-m-d";
~~~

### Options
Options are some additional informations, which can completely change the behavior of property. Each option must be prefixed with `m:` and consists of key name and values splitted by `|`.


#### Primary
Represents some kind of *foreign key* similar to relational database and every entity can be identified by it. Usually some `id` column in your database for example.

> Only one property can be primary but entity can be used without primary.

~~~ php
/**
 * @property integer $id m:primary
 */
class User extends \UniMapper\Entity
{}
~~~

#### Mapping
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

> This option is not required, so if you do not provide it, mapping will use property name as target column automatically. 

#### Computed
Some kind of virtual property, mostly dependent on other real properties so it is readonly and can not be set directly. It can be helpful in situations like price computing for example.

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