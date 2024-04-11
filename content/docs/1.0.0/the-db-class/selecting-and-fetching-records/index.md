---
title: "Db - Selecting and Fetching Records"
linkTitle: "Selecting and Fetching Records"
date: 2024-03-28T11:59:00+01:00
draft: false
description: "The Db class offers a range of methods for selecting records, specific rows, values, or the count of records. The ability to apply joins, conditions, and parameters across all these methods enhances the flexibility of your database operations."
noindex: false
comments: false
nav_weight: 200
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

This page provides a practical guide on how to use the `Db` class for selecting and fetching records from a database. The following methods of the `Db` class are covered:

- [Db::select](/docs/{{< param "doc_version">}}/db-selecting-and-fetching-records/#select)
- [Db::selectRow](/docs/{{< param "doc_version">}}/db-selecting-and-fetching-records/#selectrow)
- [Db::selectValue](/docs/{{< param "doc_version">}}/db-selecting-and-fetching-records/#selectValue)
- [Db::selectCount](/docs/{{< param "doc_version">}}/db-selecting-and-fetching-records/#selectCount)
- [Db::numRows](/docs/{{< param "doc_version">}}/db-selecting-and-fetching-records/#numRows)

<!--more-->

## Loading the Db class

To use the `Db` class, you first need to load it within the Dependency Injection (DI) container.

```php
use Migliori\PowerLitePdo\Db;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$db = $container->get(Db::class);
```

{{< separator >}}

<article>

## Select() {.mt-5}

The `Db::Select()` method prepares and executes the SQL SELECT statement in a single function call.

### Method Signature ### {#selectMethodSignature .mt-5}

```php
public function select(
    string $from,
    string|array $fields,
    ?array $where = [],
    ?array $parameters = [],
    bool|string $debug = false
): mixed
```

### Arguments Summary ### {#selectArgumentsSummary .mt-5}

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $from | {{< arguments/from type="true" >}} | {{< arguments/from description="true" >}} | {{< arguments/from examples="true" >}} |
| $fields | {{< arguments/fields type="true" >}} | {{< arguments/fields description="true" >}} | {{< arguments/fields examples="true" >}} |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |
| $parameters | {{< arguments/parameters type="true" >}} | {{< arguments/parameters description="true" >}} | {{< arguments/parameters examples="true" >}} |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#selectExamples .mt-5}

{{< heading level="4" heading="Minimal example" small="Db::Select()" >}}

```php
$db->select('users', 'name');
while ($row = $db->fetch()) {
    echo $row->name;
}
```

{{< heading level="4" heading="Selecting multiple fields" class="mt-5" small="Db::Select()" >}}

```php
$db->select('users', ['id', 'name', 'email']);
while ($row = $db->fetch()) {
    echo $row->id . ', ' . $row->name . ', ' . $row->email;
}
```

{{< heading level="4" heading="Adding a WHERE clause" class="mt-5" small="Db::Select()" >}}

```php
$db->select('users', ['id', 'name', 'email'], ['status' => 'active']);
while ($row = $db->fetch()) {
    echo $row->id . ', ' . $row->name . ', ' . $row->email;
}
```

{{< heading level="4" heading="Adding a more complex WHERE clause" class="mt-5" small="Db::Select()" >}}

```php
$db->select('users', ['id', 'name', 'email'], ['users.id >' => 10, 'users.name LIKE' => '%me%']);
while ($row = $db->fetch()) {
    echo $row->id . ', ' . $row->name . ', ' . $row->email;
}
```

{{< heading level="4" heading="Adding parameters (selectDistinct, orderBy, groupBy, limit)" class="mt-5" small="Db::Select()" >}}

```php
$db->select('users', ['id', 'name', 'email'], ['status' => 'active'], ['limit' => 10, 'orderBy' => 'name ASC']);
while ($row = $db->fetch()) {
    echo $row->id . ', ' . $row->name . ', ' . $row->email;
}
```

{{< heading level="4" heading="Using a JOIN in the $from argument" class="mt-5" small="Db::Select()" >}}

```php
$db->select('users INNER JOIN profiles ON users.id = profiles.user_id', ['users.id', 'users.name', 'users.email', 'profiles.name AS profilesName'], ['status' => 'active']);
while ($row = $db->fetch()) {
    echo $row->id . ', ' . $row->name . ', ' . $row->email . ', ' . $row->profilesName;
}
```

{{< heading level="4" heading="Using the fetchAll method" class="mt-5" small="Db::Select()" >}}

```php
$db->select('users', ['id', 'name', 'email'], ['status' => 'active']);
$rows = $db->fetchAll();
foreach ($rows as $row) {
    echo $row->id . ', ' . $row->name . ', ' . $row->email;
}
```

</article>

{{< separator >}}

<article>

## selectRow()

The `Db::SelectRow()` method combines the preparation and execution of the SQL SELECT statement into a single function call. It returns an object or array containing the fetched record based on the specified `$fetchParameters`.

### Method Signature ### {#selectRowMethodSignature .mt-5}

```php
public function selectRow(
    string $from,
    mixed $fields = '*',
    mixed $where = [],
    int $fetchParameters = PDO::FETCH_OBJ,
    bool|string $debug = false
): mixed
```

### Arguments Summary ### {#selectRowArgumentsSummary .mt-5}

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $from | {{< arguments/from type="true" >}} | {{< arguments/from description="true" >}} | {{< arguments/from examples="true" >}} |
| $fields | {{< arguments/fields type="true" >}} | {{< arguments/fields description="true" >}} | {{< arguments/fields examples="true" >}} |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |
| $fetchParameters | ?int | The PDO Fetch mode | PDO::FETCH_OBJ OR PDO::FETCH_ASSOC |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#selectRowExamples .mt-5}

{{< heading level="4" heading="Simple Use Case" small="Db::selectRow()" >}}

```php
$db = new Db();
$result = $db->selectRow('users', '*', ['id' => 1]);
echo $result->name;
```

In this example, we are selecting all fields from the 'users' table where the 'id' is 1. The result is fetched as an object.

{{< heading level="4" heading="Complex Use Case with Joins and Specific Fields" class="mt-5" small="Db::selectRow()" >}}

```php
$db = new Db();
$result = $db->selectRow('users INNER JOIN profiles ON users.id = profiles.user_id', ['users.id', 'users.name', 'profiles.name AS profilesName'], 'users.id = 1', PDO::FETCH_ASSOC);
echo $result['name'] . ' - ' . $result['profilesName'];
```

In this example, we are selecting specific fields from a join between the 'users' and 'profiles' tables where the 'id' in 'users' table is 1. The result is fetched as an associative array. The 'debug' mode is also enabled.

</article>
