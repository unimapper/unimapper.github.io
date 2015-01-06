---
layout: docs
title: Validation
permalink: /docs/reference/validation/
---

Suits perfectly to situations when you need to validate data in your model layer or developing front-end application bundled with some REST api together.
Validation syntax can be very simple or much advanced with very clear writing without any IF hell in your code.

## Rules

### Entity
~~~ php
$entity->getValidator()
    ->addRule(function(\UniMapper\Entity $entity) {
        return $entity->text === "foo";
    }, "Text must be foo!");
~~~

### Property
~~~ php
$entity->getValidator()
    ->on("text")
        ->addRule(Validator::FILLED, "Text is required!")
    ->on("email")
        ->addRule(Validator::EMAIL, "Invalid e-mail format!");
~~~

> [Computed]({{ site.baseUrl }}/docs/reference/entity/#computed) properties can not be validated!

### Nested entities
~~~ php
$order->getValidator()
    ->on("product")
        ->addRule(Validator::FILLED, "Product is required!");
$order->customer->getValidator()
    ->on("email")
        ->addRule(Validator::EMAIL, "Invalid e-mail!");
$order->customer->branchOffice->getValidator()
    ->on("phone")
        ->addRule(Validator::FILLED, "Invalid phone!");
~~~

## Conditions
~~~ php
$entity->getValidator()
    ->on("ip")
        ->addCondition(Validator::FILLED)
            ->addRule(Validator::IP, "Invalid IP format!")
        ->endCondition()
~~~

## Usage
You can set validation rules to every single entity instance by calling `getValidator()` method.
