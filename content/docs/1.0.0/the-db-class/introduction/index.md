---
title: "Db - Introduction"
linkTitle: "Introduction"
date: 2024-03-29T10:09:39+01:00
draft: false
description: "Learn about the Db class, how to instantiate it, and how to access its child classes PDO and Query Builder."
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

The `Db` class is a wrapper around the PHP Data Objects (PDO) extension and serves as a database abstraction layer to provide a simple, consistent interface for interacting with different types of databases.

It is designed to use procedural methods and is responsible for establishing a connection to the database, executing queries, and returning results. The `Db` class uses a [`DriverBase`](/docs/{{< param "doc_version">}}/db-introduction/#pdo-driver-manager) instance for the connection and a [`QueryBuilder`](/docs/{{< param "doc_version">}}/the-querybuilder/) instance for building and executing SQL queries.

In summary, the `Db` class provides a procedural interface for executing SQL queries and managing the database connection, while the `QueryBuilder` class provides a fluent interface for building SQL queries.

## Instantiating the Db class

The `Db` class is instantiated using Dependency Injection (DI) via the `bootstrap.php` file. Here's an example of how to do it:

```php
use Migliori\PowerLitePdo\Db;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$db = $container->get(Db::class);
```

This code first includes the `bootstrap.php` file, which sets up the DI container. Then, it retrieves an instance of the `Db` class from the container.

## Accessing the PDO child object

The `Db` class has a protected property `$pdo` that holds the PDO instance. This PDO instance is used to execute queries against the database. Here's an example of how to retrieve the PDO instance:

```php
$pdo = $db->getPdo();
```

This code calls the `getPdo()` method on the `Db` instance to retrieve the PDO instance.

## Accessing the Query Builder child object

The `Db` class also has a protected property `$queryBuilder` that holds an instance of the Query Builder. The Query Builder provides a fluent interface to build SQL queries.

If you ever need to switch to using the Query Builder instance and utilize its fluent style instead of the Db class methods for constructing your queries, here's how you can proceed:

```php
$queryBuilder = $db->getQueryBuilder();
```

This code calls the `getQueryBuilder()` method on the `Db` instance to retrieve the Query Builder instance.

## PDO Driver Manager

The `DriverManager` class is responsible for managing the PDO drivers. It provides a method to get the appropriate driver based on the database type. The `DriverManager` class is used internally by the `Db` class to manage the PDO connection. You can find more details about the `DriverManager` class in the DriverManager.php file.
