---
layout: docs
title: Create app
permalink: /docs/get-started/create-app/
prev_section: /get-started/task
next_section: /get-started/entities
---

This application will be very simple, without any frameworks for the best example of library usage.

## index.php
Create a master file to which the user will be directed on.

## Libraries
If you're using composer as recommended from [install chapter]({{ site.baseeurl}}/docs/get-started/install) define composer package in `composer.json` and run `composer install`.

**./composer.json**

~~~ json
{
    "name": "bauer01/get-started",
    "type": "project",
    "description": "The ORM demonstration",
    "keywords": ["php", "mapping", "data", "orm", "database", "example"],
    "license": ["MIT"],
    "authors": [
        {
            "name": "Bronislav Sedlak",
            "homepage": "http://github.com/bauer01"
        }
    ],
    "require": {
        "php": ">=5.4.0",
        "bauer01/unimapper": "@dev"
    },
    "minimum-stability": "dev"
}
~~~

Then load require `autoload.php`.

**./index.php**

~~~ php
require_once __DIR__ . '/vendor/autoload.php';
~~~

> If your are not using composer, make sure you download and load all necessary library files manually instead.