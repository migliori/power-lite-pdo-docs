---
title: "Db - Insert Update Delete"
linkTitle: "Insert Update Delete"
date: 2024-03-29T08:12:08+01:00
draft: false
description: "PowerLite PDO: Learn how to manipulate your database records using insert, update, and delete operations."
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

This page provides a practical guide on how to execute SQL queries using the `Db` class in the PowerLitePdo library. We will cover the following methods:

- [Db::insert](/docs/{{< param "doc_version">}}/db-insert-update-delete/#insert)
- [Db::update](/docs/{{< param "doc_version">}}/db-insert-update-delete/#update)
- [Db::delete](/docs/{{< param "doc_version">}}/db-insert-update-delete/#delete)

<!--more-->

## Loading the Db class within the DI container

To use the Db class, you first need to load it within the Dependency Injection (DI) container. Here's how you can do it:

```php
use Migliori\PowerLitePdo\Db;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$db = $container->get(Db::class);
```

{{< separator >}}

<article>

## Db::insert() {#insert .mt-5}

The `Db::insert` method inserts a new record into a specified table. The `$values` argument is an associative array where the keys represent the column names and the values represent the corresponding values to be inserted. The `$debug` argument controls whether the insert operation is executed and how debugging information is handled. It returns the number of affected rows or false on failure.

```php
public function insert(
    string $table,
    array $values,
    bool|string $debug = false
) : bool|int
```

### Arguments Summary ### {#insertArgumentsSummary .mt-5}

| Argument | Type | Description | Example |
| --- | --- | --- | --- |
| $table | string | The name of the table into which a new record will be inserted. | <pre class="{{< param "arguments_code_class">}}">'customers'</pre> |
| $values | array<string, mixed> | An associative array containing the fields and values to be inserted. | <pre class="{{< param "arguments_code_class">}}">['name' => 'Cathy', 'city' => 'Cardiff']</pre> |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#insertExamples .mt-5}

{{< heading level="4" heading="INSERT" small="Db::insert()" >}}

```php
$table = 'customers';
$values = ['id' => null, 'name' => 'John Doe', 'city' => 'New York'];

// Send the query and retrieve the number of affected rows
$result = $db->insert($table, $values);

// Get the last insert id
$lastInsertId = $db->getLastInsertId();
```

In this example, a new customer named 'John Doe' from 'New York' is inserted into the 'customers' table. The insert operation is executed and no debugging information is displayed.

{{< heading level="4" heading="INSERT - debug mode enabled" small="Db::insert()" >}}

```php
$table = 'orders';
$values = ['id' => null, 'customer_id' => 1, 'product_id' => 101, 'quantity' => 3];

// Simulate the INSERT query and retrieve the number of affected rows
$result = $db->insert($table, $values, true);

// Get the last insert id
$lastInsertId = $db->getLastInsertId();
```

In this example, a new order is inserted into the 'orders' table. The insert operation is not executed, but the query is displayed for debugging purposes.
</article>

{{< separator >}}

<article>

## Db::update() {#update .mt-5}

This method is used to update records in a database table. It returns the number of affected rows or false on failure.

### Method Signature ### {#updateMethodSignature .mt-5}

```php
public function update(string $table,
    array $data,
    $where = null,
    bool|string $debug = false
): bool|int
```

### Arguments Summary ### {#updateArgumentsSummary .mt-5}

| Argument | Type | Description | Example |
| --- | --- | --- | --- |
| $table | string | The name of the table to update. | <pre class="{{< param "arguments_code_class">}}">users<br>orders</pre> |
| $data | array | An associative array where the key is the column name and the value is the new value. | <pre class="{{< param "arguments_code_class">}}">['name' => 'newuser', 'email' => 'newuser@example.com']</pre> |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#updateExamples .mt-5}

{{< heading level="4" heading="UPDATE" small="Db::update()" >}}

```php
// Update a single record
$result = $db->update('users', ['name' => 'newuser'], 'id = 1');

// Simulate an update query using the $debug parameter for debugging purposes. The update operation is not actually executed.
$result = $db->update('orders', ['name' => 'newuser'], 'id = 1', true);
```

</article>

{{< separator >}}

<article>

{{< separator >}}

<article>

## delete() {#delete .mt-5}

This method is used to delete records from a database table. It returns the number of affected rows or false on failure.

### Method Signature ### {#deleteMethodSignature .mt-5}

```php
public function delete(
    string $table,
    array<int|string, mixed>|string $where,
    bool|string $debug = false
) : bool|int
```

### Arguments Summary ### {#deleteArgumentsSummary .mt-5}

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $table | string | The name of the table to delete records from. | <pre class="{{< param "arguments_code_class">}}">users<br>orders</pre> |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#deleteExamples .mt-5}

{{< heading level="4" heading="DELETE" small="Db::delete()" >}}

```php
// Delete a user with id 1
$db->delete('users', ['id' => 1]);

// Simulate a deletion with the $debug parameter for debugging purposes. The delete operation is not actually executed.
$db->delete('orders', 'id = 100', true);
```

</article>
