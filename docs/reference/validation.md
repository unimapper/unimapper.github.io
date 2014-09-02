---
layout: docs
title: Validation
permalink: /docs/reference/validation/
---

Another attractive feature is validation. We believe that validation belongs to the model, all in one place. And with this library you can really create advanced validation with very clear writing. So no more `IF` hell in your code :-).

## Rules

### Entity
~~~ php
$entity->getValidator()
    ->addRule(function(\UniMapper\Entity $entity) {
        return $entity->text === "foo";
    }, "Text must be foo!")
~~~

### Property
~~~ php
$entity->getValidator()
    ->on("text")
        ->addRule(Validator::FILLED, "Text is required!")
    ->on("email")
        ->addRule(Validator::EMAIL, "Invalid e-mail format!");
~~~

> Remember! [Computed]({{ site.baseUrl }}/docs/reference/entity/#computed) properties can not be validated!

### Nested entities

## Conditions

## Messages
