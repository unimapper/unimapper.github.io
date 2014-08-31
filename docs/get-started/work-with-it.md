---
layout: docs
title: Work with it
prev_section: /get-started/describe-your-data
---

Nice! You are almost at the finish. You only need to load orders now. It can be done in [repository]({{ site.baseurl }}/docs/reference/repository/).

**/model/repository/Order.php**

~~~ php
namespace MyApp\Model\Repository;

class Order extends \UniMapper\Repository
{
    public function find()
    {
        return $this->query()->find()->execute();
    }
}
~~~

**/index.php**

~~~ php
$orders = new MyApp\Model\Repository\Order;
$orders->registerAdapter($databaseAdapter);

foreach ($orders->find() as $order) {
	echo $order->company;
}
~~~

Now you can go home, the work is done for today! ;-)