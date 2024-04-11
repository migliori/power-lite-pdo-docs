---
title: "Pagination - Select and Paginate Results"
linkTitle: "Pagination"
date: 2024-03-29T12:00:05+01:00
draft: false
description: "Selecting and Paginating Results in PowerLite PDO - Step-by-step guide on how to use PowerLite PDO for efficient record selection and pagination."
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

This guide provides a step-by-step tutorial on how to use PowerLite PDO for efficient record selection and pagination. We will be using the `Pagination` class from the PowerLite PDO library.

<!--more-->

## Step 1:Loading the Pagination class

To use the `Pagination` class, you first need to load it within the Dependency Injection (DI) container.

```php
use Migliori\PowerLitePdo\Pagination;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$pagination = $container->get(Pagination::class);
```

## Step 2: Selecting Records

The `Pagination` class provides a `select` method to fetch data from the database.

```php
public function select(
    string $from,
    $fields,
    $where = [],
    array $parameters = [],
    $debug = false
): self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $from | {{< arguments/from type="true" >}} | {{< arguments/from description="true" >}} | {{< arguments/from examples="true" >}} |
| $fields | {{< arguments/fields type="true" >}} | {{< arguments/fields description="true" >}} | {{< arguments/fields examples="true" >}} |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |
| $parameters | {{< arguments/parameters type="true" >}} | {{< arguments/parameters description="true" >}} | {{< arguments/parameters examples="true" >}} |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#selectRowExamples .mt-5}

```php
$from = 'users'; // The SELECT FROM clause
$fields = ['id', 'name', 'email']; // The columns you want to select
$where = ['status' => 'active']; // The conditions for the WHERE clause
$parameters = ['orderBy' => 'name'];
$pagination->select($from, $fields, $where, $parameters);
```

## Step 3: Fetching and Displaying Records

After selecting the records, you can fetch and display them using a while loop:

```php
$records = [];
while ($record = $pagination->fetch()) {
    $records[] = $record->id . ', ' . $record->username . ', ' . $record->email;
}
echo implode('<br>', $records);
```

This code fetches each record and adds it to the `$records` array. The records are then displayed as a string, with each record separated by a line break.

## Step 4: Paginating Results

The `Pagination` class also provides a `pagine` method to generate pagination links. Here's how to use it:

```php
$url = '/examples/pagination-examples.php'; // The URL for the pagination links
echo $pagination->pagine($url);
```

This code generates pagination links for the URL `/examples/pagination-examples.php`.

For more advanced usage, such as setting the number of records per page or customizing the pagination links, refer to the next page about [Pagination Options](/docs/{{< param "doc_version">}}/pagination-options/).

Please note that this guide provides a basic overview of how to use the `Pagination` class. For more detailed examples, refer to the `examples/pagination-examples.php` file.
