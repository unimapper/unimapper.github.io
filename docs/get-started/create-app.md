---
layout: docs
title: Create app
permalink: /docs/get-started/create-app/
prev_section: /get-started/task
next_section: /get-started/entities
---

## index.php
Create a master file to which the user will be directed.

## Libraries
If you're using recommended composer, load all required libraries as the first step.

**./index.php**

~~~ php
require_once __DIR__ . '/vendor/autoload.php';
~~~

If not, make sure you load all the necessary files manually.