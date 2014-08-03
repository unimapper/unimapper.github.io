---
layout: docs
title: Work with it
permalink: /docs/get-started/work-with-it/
prev_section: /get-started/describe-your-data
---

Nice! You are almost at the finish. You only need to load orders now. It can be done in [repository]({{ site.baseurl }}/docs/reference/repository/).

**/model/repository/Order.php**

~~~ php
namespace MyApp\Model\Repository;

class Order extends \UniMapper\Repository
{
    public function findAll()
    {
        return $this->query()->findAll()->execute();
    }
}
~~~

**/index.php**

~~~ php
$orders = new MyApp\Model\Repository\Order;
$orders->registerMapper($databaseMapper);

foreach ($orders->findAll() as $order) {
	echo $order->company;
}
~~~

Now you can go home, the work is done for today! ;-)