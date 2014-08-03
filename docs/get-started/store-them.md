---
layout: docs
title: Store them
permalink: /docs/get-started/store-them/
prev_section: /get-started/describe-your-data
next_section: /get-started/work-with-it
---

The next thing you need is something that can user create, update, delete or retrieve from your data storage. It is generally assumed that the data will be stored in some database or behind some REST API. No problem, precisely for this purpose are [mappers]({{ site.baseurl }}/docs/reference/mapper/). To avoid having to create a new mapper from scratch, you can use some mapper from [extensions]({{ site.baseurl }}/docs/extensions/browse/).

In this case we prefer a database so choosing our favorite [Dibi]({{ site.baseurl }}/docs/extensions/browse/#dibi) can be the best choice (excellent abstraction layer with different database types support). So put DibiMapper.php to **/model/mapper/DibiMapper.php**.

**index.php**

~~~ php
$connection = new \DibiConnection(["driver" => "mysql", "host" => "localhost", "db" => "mydb"]);
$databaseMapper = new UniMapper\Mapper\DibiMapper($connection, "Database");
~~~

Now you have defined mapper with database connection. But you must tell your entities how to connect. It can be done with `@mapper` definition. Complete your entities like this.

**/model/entity/User.php**

~~~ php
 * @mapper Database(users)
 *
 * @property integer  $id        m:primary
 * @property string   $username
 * @property DateTime $createdOn
~~~

.. and this.

**/model/entity/Order.php**

~~~ php
 * @mapper Database(orders)
 *
 * @property string   $code      m:primary
 * @property string   $company
 * @property DateTime $createdOn
~~~