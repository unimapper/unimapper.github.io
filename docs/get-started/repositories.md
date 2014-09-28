---
layout: docs
title: Repositories
permalink: /docs/get-started/repositories/
prev_section: /get-started/connections
---

For accessing our data we use [repositories]({{ site.baseurl }}/docs/reference/repository).

**./Model/Repository/OrderRepository.php**

~~~ php
namespace GetStarted\Model\Repository;

class OrderRepository extends \UniMapper\Repository
{}
~~~

**./index.php**

~~~ php
require_once __DIR__ . '/../../model/repository/OrderRepository.php';

$orderRepository = new \GetStarted\Model\Repository\OrderRepository;
$orderRepository->registerAdapter($dibiAdapter);
$orderRepository->registerAdapter($mongoAdapter);
~~~
