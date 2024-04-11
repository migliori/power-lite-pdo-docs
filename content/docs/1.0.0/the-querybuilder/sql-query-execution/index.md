---
title: "Query Builder - SQL Query Execution"
linkTitle: "SQL Query Execution"
date: 2024-03-29T07:47:15+01:00
draft: false
description: "PowerLite PDO's QueryBuilder offers a streamlined approach to SQL query execution. Learn the essentials of creating and executing SQL queries."
noindex: false
comments: false
nav_weight: 300
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

This page provides a comprehensive guide on how to use the `QueryBuilder::query()` method to execute SQL queries using prepared or non-prepared SQL strings.

<!--more-->

## Table of Contents

- [Loading the QueryBuilder Class](/docs/{{< param "doc_version">}}/query-builder-sql-query-execution/#loading-the-querybuilder-class)
- [Executing Raw SQL Queries](/docs/{{< param "doc_version">}}/query-builder-sql-query-execution/#executing-raw-sql-queries)
- [Executing Prepared SQL Queries](/docs/{{< param "doc_version">}}/query-builder-sql-query-execution/#executing-prepared-sql-queries)

## Loading the QueryBuilder Class

Before you can use the `QueryBuilder` class, you need to load it within the Dependency Injection (DI) container.

```php
use Migliori\PowerLitePdo\Query\QueryBuilder;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$queryBuilder = $container->get(QueryBuilder::class);
```

{{< separator >}}

<article>

## Executing Raw SQL Queries {.mt-5}

The `query` method in the `QueryBuilder` class is used to execute a raw SQL query. It takes a string argument representing the SQL query to be executed.

```php
public function query(string $sql): self
```

### Arguments Summary ### {#queryArgumentsSummary .mt-5}

| Argument Name | Type | Description |
| --- | --- | --- |
| $sql | string | The SQL query string to be executed |

**Warning**: Using raw SQL queries can expose your application to SQL Injection attacks. It's recommended to use prepared SQL queries for better security. See the next section for more details.

### QueryBuilder::execute {.mt-5}

The `execute` method is used to execute the query.

```php
public function execute() : self
```

### Examples ### {#queryExamples .mt-5}

{{< heading level="4" heading="SELECT query with non-prepared SQL" class="mt-5" small="Db::query()" >}}

```php
$queryBuilder->query("SELECT * FROM users WHERE name = 'John'")->execute();
```

{{< heading level="4" heading="UPDATE query with non-prepared SQL" class="mt-5" small="Db::query()" >}}

```php
$queryBuilder->query("UPDATE users SET name = 'Jane' WHERE id = 1")->execute();
```

</article>

{{< separator >}}

<article>

## Executing Prepared SQL Queries {.mt-5}

The `query` method also supports prepared SQL queries. This is achieved by using placeholders in the SQL query string and passing the actual values separately. The `placeholders` method is used to pass the actual values for the placeholders.

### Arguments Summary ### {#queryPreparedArgumentsSummary .mt-5}

```php
public function query(string $sql): self
public function placeholders(array $values): self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $sql | string | The SQL query string with placeholders | <pre class="{{< param "arguments_code_class">}}">'SELECT * FROM users WHERE name = :name'<br>'UPDATE users SET name = :newName WHERE id = :id'</pre> |
| $values | array | The actual values for the placeholders | <pre class="{{< param "arguments_code_class">}}">['name' => 'John Doe']<br>['newName' => 'Jane Doe', 'id' => 10]</pre> |

### Examples ### {#queryPreparedExamples .mt-5}

{{< heading level="4" heading="SELECT query with prepared SQL" class="mt-5" small="Db::query()" >}}

```php
$queryBuilder = new QueryBuilder();
$queryBuilder->query("SELECT * FROM users WHERE name = :name")
             ->placeholders(['name' => 'John'])->execute();
```

{{< heading level="4" heading="UPDATE query with prepared SQL" class="mt-5" small="Db::query()" >}}

```php
$queryBuilder = new QueryBuilder();
$queryBuilder->query("UPDATE users SET name = :newName WHERE id = :id")
             ->placeholders(['newName' => 'Jane', 'id' => 1])->execute();
```

</article>
