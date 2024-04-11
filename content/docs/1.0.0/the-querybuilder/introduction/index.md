---
title: "Query Builder - Introduction"
linkTitle: "Introduction"
date: 2024-03-29T10:09:39+01:00
draft: false
description: "The QueryBuilder class enables fluent database operations with methods for record selection, joins, conditions, and parameters. Streamline your SQL queries with this versatile tool."
noindex: false
comments: false
nav_weight: 100
series:
  - Docs
categories:
#  -
tags:
#  -
images:
#  -
# menu:
#   main:
#     weight: 100
#     params:
#       icon:
#         vendor: bs
#         name: book
#         color: '#e24d0e'
---

The PowerLite PDO QueryBuilder is a powerful tool in the Migliori PowerLitePdo library. It provides an easy-to-use, fluent interface for creating and executing database queries. Unlike the [`Db`](command:_github.copilot.openSymbolInFile?%5B%22src%2FDb.php%22%2C%22Db%22%5D "src/Db.php") class, which provides a direct interface to the database, the QueryBuilder allows you to construct queries programmatically, providing a more flexible and intuitive approach to data manipulation.

<!--more-->

## Loading the QueryBuilder

The QueryBuilder can be loaded using Dependency Injection (DI) as shown in the example below:

```php
use Migliori\PowerLitePdo\Query\QueryBuilder;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$queryBuilder = $container->get(QueryBuilder::class);
```

## Chaining Methods

One of the key features of the QueryBuilder is the ability to chain methods together, culminating in the final "execute" method. This provides a clean, readable syntax for building up complex queries. Here's an example:

```php
$results = $queryBuilder
->select('*')
->from('users')
->where(['status' => 'active'])
->orderBy('name', 'ASC')
->execute();

while ($record = $queryBuilder->fetch()) {
    echo $record->id . ', ' . $record->name . ', ' . $record->email;
}
```

In this example, we're selecting all active users and ordering the results by name in ascending order.

## The Power of PDO

Under the hood, the QueryBuilder uses the PHP Data Objects (PDO) extension to interact with the database. This provides a consistent interface for accessing databases, and allows the QueryBuilder to support any database that PDO does.

## PDO Driver Manager

The `DriverManager` class is responsible for managing the PDO drivers. It provides a method to get the appropriate driver based on the database type. The `DriverManager` class is used internally by the `Db` class to manage the PDO connection. You can find more details about the `DriverManager` class in the DriverManager.php file.

## Next Steps

This introduction has only scratched the surface of what the QueryBuilder can do. In the following sections of the documentation, we'll dive deeper into its capabilities, with detailed examples and explanations of its various methods and features. From basic CRUD operations to complex joins and subqueries, the QueryBuilder has you covered.
