---
layout: post
title: "Faster, harder, reflection!"
author: bauer01
categories: [development]
---

It's been a long time I post something new, shame on me! :-) But there was a lot of things to do with this library and the next big thing is entity reflection refactoring.

## Problem
Stumbling block of entire library was demanding on system resources during the reflection load. I made some performance test with this benchmark and the result was something between ~ `20s / 70 MB` on my PC, which was terrible.

## After refactoring
But after a few cups of coffee and one sleepless saturday night, came the results in the form of ~ `5s / 19 MB`. Test focus on data *(~300000 rows)* stored in MySQL database, which are joined with 1:N and M:N relation, so I choosed our [Dibi extension](https://github.com/unimapper/dibi). After all, you can test it on your own from [here](https://github.com/bauer01/db-benchmark/tree/unimapper).

## What I actually did?
The problem was, that almost every attempt to find out some information about entity meant creating a new instance of reflection, so I made a lazy creation of related entity reflections. That means, every entity reflection brings an array with related entity reflections from its property definitions.

**Example:**

~~~ php
namespace Model;

/**
 * @adapter MyAdapter(table_name)
 *
 * @property Child $entity
 */
class MyEntity extends \UniMapper\Entity
{}

$reflection = new UniMapper\Reflection\Entity("Model\MyEntity");

var_dump($reflection->getRelated());

// Prints following:
// array( "Model\Child" => ... /* Child entity reflection object */ )
~~~

Yep, there is a lot of todos with reflection, but for starters it is not bad.