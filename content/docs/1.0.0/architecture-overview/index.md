---
title: "Architecture Overview"
# linkTitle:
date: 2024-03-28T08:07:17+01:00
draft: false
description: "Understand PowerLite PDO's Architecture - Discover how our PHP database abstraction layer is structured for optimal performance and flexibility."
noindex: false
comments: false
nav_weight: 10
nav_icon:
  vendor: fas
  name: sitemap
  color: '#548289'
series:
  - Docs
categories:
#  -
tags:
#  -
images:
  - /images/powerlite-pdo-logo-horizontal.png
#  -
# menu:
#   main:
#     weight: 100
#     params:
#       icon:
#         vendor: fas
#         name: book
#         color: '#e24d0e'
---

The PowerLite PDO library provides a lightweight and powerful abstraction layer for PHP's PDO (PHP Data Objects) extension. The library is designed with a clear separation of concerns in mind, and it uses Dependency Injection (DI) to manage dependencies between different parts of the system.

## Structure and Logic

The project is organized into several key components:

- **Db**: `src/Db.php` Main interface for interacting with the database. It handles connection management, query execution, and result processing. It uses the `DriverManager` to establish a connection to the database and the `QueryBuilder` to execute SQL queries.

- **QueryBuilder**: `src/Query/QueryBuilder.php` Used to build SQL queries in a flexible and extensible way. The QueryBuilder class is not only used internally by the Db class, but it is also designed to be a standalone fluent query builder, allowing developers to build SQL queries in a flexible and extensible manner. The `QueryBuilder` uses the `Parameters` and `Where` classes to handle query parameters and WHERE clauses, respectively. The results of the queries are processed by the `Result` class.

- **Pagination**: `src/Pagination.php` Used to handle pagination of query results. It works in conjunction with the `Db` and `QueryBuilder` classes to provide paginated results for queries.

- **DriverManager**: `src/DriverManager.php` Responsible for managing the database drivers. It provides a method to get a connection to the database using the specified driver. The `DriverManager` is used by the `Db` and `QueryBuilder` classes to establish a connection to the database.

These classes work together to provide a flexible and extensible database abstraction layer. The `Db` class is the main entry point, using the `DriverManager` to establish a connection and the `QueryBuilder` to execute queries. The `Pagination` class is used to paginate the results of these queries.

## Dependency Injection

PowerLite PDO uses Dependency Injection (DI) to manage dependencies between different parts of the system. The DI container is configured in a bootstrap file, and a separate connection file is used to manage database connections.

## Initializing Database, QueryBuilder, and Pagination Instances

In PowerLite PDO, instances of `Db`, `QueryBuilder`, and `Pagination` are loaded from the Dependency Injection (DI) container. This is done in the `config.php` file.

To connect to your database and start using PowerLite PDO, you need to enter your connection parameters in the dedicated file, load the Dependency Injection (DI) container, and then load the class you are using.

Everything is explained here: [/docs/{{< param "doc_version" >}}/getting-started/](/docs/{{< param "doc_version" >}}/getting-started/)
