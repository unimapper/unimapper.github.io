---
layout: docs
title: Describe your data
permalink: /docs/get-started/describe-your-data/
prev_section: /get-started/install
next_section: /get-started/store-them
---

One fine day your boss arrives and tells you.

> Hey you! Users in this company want to see new orders from today. Do it quickly!

And you should answer:

> No worries, piece of cake ;-)

## Directory structure

First of all, you need to realize your app structure. Maybe you heared about models, active record and stuff like that.
but it is better to separate logic entities, repository and queries.

~~~ shell
index.php
/model
../entity
../mapper
../repository
~~~

## Entities
Then you must describe objects you will work with. These objects are called [entities]({{ site.baseurl }}/docs/reference/entity/) and as your boss said, there are users ..

**/model/entity/User.php**

~~~ php
namespace MyApp\Model\Entity;

/**
 * @property integer  $id        m:primary
 * @property string   $username
 * @property DateTime $createdOn
 */
class User extends \UniMapper\Entity
{}
~~~

.. and they want to see orders.

**/model/entity/Order.php**

~~~ php
namespace MyApp\Model\Entity;

/**
 * @property string   $code      m:primary
 * @property string   $company
 * @property DateTime $createdOn
 */
class Order extends \UniMapper\Entity
{}
~~~