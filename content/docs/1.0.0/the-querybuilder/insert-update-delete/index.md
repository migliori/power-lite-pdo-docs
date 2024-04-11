---
title: "Query Builder - Insert Update Delete"
linkTitle: "Insert Update Delete"
date: 2024-03-29T08:12:08+01:00
draft: false
description: "The QueryBuilder provides a robust platform for data fetching and conversion. Understand the key principles for effective data manipulation."
noindex: false
comments: false
nav_weight: 400
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

This page provides a comprehensive guide on how to use the `QueryBuilder` class for `insert`, `update`, and `delete` operations in your database. The guide includes practical code samples for each operation.

## Table of Contents

1. [Loading the QueryBuilder Class](/docs/{{< param "doc_version">}}/query-builder-insert-update-delete/#loading-the-querybuilder-class)
2. [Insert](/docs/{{< param "doc_version">}}/query-builder-insert-update-delete/#insert-records)
3. [Update](/docs/{{< param "doc_version">}}/query-builder-insert-update-delete/#update-records)
4. [Delete](/docs/{{< param "doc_version">}}/query-builder-insert-update-delete/#delete-records)

<!--more-->

## Loading the QueryBuilder Class

Before you can use the `QueryBuilder` class, you need to load it within the Dependency Injection (DI) container.

```php
use Migliori\PowerLitePdo\Query\QueryBuilder;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$queryBuilder = $container->get(QueryBuilder::class);
```

{{< separator >}}

<article>

## Insert Records

### Method Signature ### {#insertMethodSignature .mt-5}

```php
public function insert(string $table, array $values) : self
```

### Arguments Summary ### {#insertArgumentsSummary .mt-5}

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $table | string | The name of the table to insert records into. | <pre class="{{< param "arguments_code_class">}}">'users'</pre> |
| $values | array | An associative array of column names and their corresponding values. | <pre class="{{< param "arguments_code_class">}}">['name' => 'John Doe', 'email' => 'john.doe@example.com']</pre> |

### QueryBuilder::execute {.mt-5}

The `execute` method is used to execute the query.

```php
public function execute() : self
```

### Examples ### {#insertExamples .mt-5}

```php
$queryBuilder->insert('users', ['name' => 'John Doe', 'email' => 'john.doe@example.com'])->execute();
```

</article>

{{< separator >}}

<article>

## Update Records

### Method Signature ### {#updateMethodSignature .mt-5}

```php
public function update(string $table, array $values, array $where) : self
```

### Arguments Summary ### {#updateArgumentsSummary .mt-5}

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $table | string | The name of the table to update records in. | <pre class="{{< param "arguments_code_class">}}">'users'</pre> |
| $values | array | An associative array of column names and their new values. | <pre class="{{< param "arguments_code_class">}}">['name' => 'Jane Doe', 'status' => 'active']</pre> |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |

### Examples of Use ### {#updateExamples .mt-5}

```php
$queryBuilder->update('users', ['name' => 'Jane Doe'], ['id' => 1])->execute();
```

</article>

{{< separator >}}

<article>

## Delete Records

### Method Signature ### {#deleteMethodSignature .mt-5}

```php
public function delete(string $table, array $where) : self
```

### Arguments Summary ### {#deleteArgumentsSummary .mt-5}

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $table | string | The name of the table to delete records from. | <pre class="{{< param "arguments_code_class">}}">'users'</pre> |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |

### Examples ### {#deleteExamples .mt-5}

```php
$queryBuilder->delete('users', ['id' => 1])->execute();
```

</article>

{{< separator >}}

<article>

## Debugging

See [Debugging](/docs/{{< param "doc_version">}}/debugging/)

</article>
