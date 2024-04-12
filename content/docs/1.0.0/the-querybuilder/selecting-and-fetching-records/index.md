---
title: "Query Builder - Selecting and Fetching Records"
linkTitle: "Selecting and Fetching Records"
date: 2024-03-28T11:59:00+01:00
draft: false
description: "The QueryBuilder provides fluent methods for record selection, with added flexibility for joins, conditions, and parameters. Enhance your database operations with its comprehensive selection capabilities."

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
#         vendor: fas
#         name: book
#         color: '#e24d0e'
---

This page provides a comprehensive guide on how to select records from a database and fetch the results with the Query Builder.

<!--more-->

## Table of Contents

1. [Loading the QueryBuilder Class](/docs/{{< param "doc_version">}}/query-builder-selecting-and-fetching-records/#loading-the-querybuilder-class)
2. [Selecting Records](/docs/{{< param "doc_version">}}/query-builder-selecting-and-fetching-records/#selecting-records)
    1. [Basics of Record Selection](/docs/{{< param "doc_version">}}/query-builder-selecting-and-fetching-records/#basics-of-record-selection)
    2. [Retrieving the Results](/docs/{{< param "doc_version">}}/query-builder-selecting-and-fetching-records/#retrieving-the-results)
    3. [Adding Parameters](/docs/{{< param "doc_version">}}/query-builder-selecting-and-fetching-records/#adding-parameters)

## Loading the QueryBuilder Class

Before you can use the `QueryBuilder` class, you need to load it within the Dependency Injection (DI) container.

```php
use Migliori\PowerLitePdo\Query\QueryBuilder;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$queryBuilder = $container->get(QueryBuilder::class);
```

{{< separator >}}

## Selecting Records

This article will guide you through the process of selecting records using the `QueryBuilder` class in the PowerLitePdo library. We will cover the basics of record selection, retrieving the results, and adding parameters.

<article>

### Basics of Record Selection ### {.mt-5}

#### QueryBuilder::from

The `from` method is used to specify the table from which to select records. It can also include MySQL joins.

```php
public function from(string $from) : self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $from | {{< arguments/from type="true" >}} | {{< arguments/from description="true" >}} | {{< arguments/from examples="true" >}} |

#### QueryBuilder::where {.mt-5}

The `where` method is used to add conditions to the query.

```php
public function where(array $conditions) : self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $where | {{< arguments/where type="true" >}} | {{< arguments/where description="true" >}} | {{< arguments/where examples="true" >}} |

#### QueryBuilder::execute {.mt-5}

The `execute` method is used to execute the query.

```php
public function execute() : self
```

{{< heading level="4" heading="Examples" class="mt-5" small="QueryBuilder::Select()" >}}

```php
$queryBuilder->select(['id', 'name', 'email'])->from('users')->where(['status' => 'active'])->execute();

$queryBuilder->select(['users.id', 'users.name', 'orders.order_date'])->from('users INNER JOIN orders ON users.id = orders.user_id')->where(['users.status' => 'active'])->execute();
```

</article>

{{< separator >}}

<article>

### Retrieving the Results ### {.mt-5}

#### QueryBuilder::fetch

Fetches the next row from a result set and returns it according to the $fetchParameters format.

```php
public function fetch(int $fetchParameters = PDO::FETCH_OBJ): mixed
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $fetchParameters | ?int | The PDO Fetch mode | <pre class="{{< param "arguments_code_class">}}">PDO::FETCH_OBJ<br>PDO::FETCH_ASSOC</pre> |

{{< heading level="4" heading="QueryBuilder fetch() example" class="mt-5" small="QueryBuilder::fetch()" >}}

```php
$queryBuilder->select(['id', 'name', 'email'])->from('users')->where(['status' => 'active'])->execute();

while ($record = $queryBuilder->fetch()) {
    echo $record->id . ', ' . $record->name . ', ' . $record->email;
}
```

#### QueryBuilder::fetchAll {.mt-5}

Fetches all rows from a result set and return them according to the $fetchParameters format.

```php
public function fetchAll(int $fetchParameters = PDO::FETCH_OBJ) : mixed
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $fetchParameters | ?int | The PDO fetch style record options | <pre class="{{< param "arguments_code_class">}}">PDO::FETCH_OBJ<br>PDO::FETCH_ASSOC</pre> |

{{< heading level="4" heading="QueryBuilder fetchAll() example" small="QueryBuilder::fetchAll()" >}}

```php
$queryBuilder->select(['id', 'name', 'email'])->from('users')->where(['status' => 'active'])->execute();

$records = $queryBuilder->fetchAll();
```

</article>

{{< separator >}}

<article>

### Converting a records set into an HTML table

#### QueryBuilder::getHTML() {.mt-5}

The `QueryBuilder::getHTML` method is used to convert a records set into an HTML table.

#### Method Signature ### {#getHTMLMethodSignature .mt-5}

```php
public function getHTML(
    array $records,
    bool $showCount = true,
    ?string $tableAttr = null,
    ?string $thAttr = null,
    ?string $tdAttr = null
): string
```

#### Arguments Summary ### {#getHTMLArgumentsSummary .mt-5}

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $records | array | The records set - can be an array or array of objects according to the fetch parameters. | <pre class="{{< param "arguments_code_class">}}">[['name' => 'John', 'age' => 30], ['name' => 'Jane', 'age' => 25]]<br>[new User('John', 30), new User('Jane', 25)]</pre> |
| $showCount | ?bool | True if you want to show the row count, false if you do not want to show the count. Default is true. | <pre class="{{< param "arguments_code_class">}}">true<br>false</pre> |
| $tableAttr | ?string | Comma separated attributes for the table. | <pre class="{{< param "arguments_code_class">}}">'class=my-class, style=color:#222'</pre> |
| $thAttr | ?string | Comma separated attributes for the header row. | <pre class="{{< param "arguments_code_class">}}">'class=my-class, style=font-weight:bold'</pre> |
| $tdAttr | ?string | Comma separated attributes for the cells. | <pre class="{{< param "arguments_code_class">}}">'class=my-class, style=font-weight:normal'</pre> |

The method returns a string containing an HTML table with all records listed.

{{< heading level="4" heading="Basic example" class="mt-5" small="QueryBuilder::getHTML()" >}}

```php
$queryBuilder->select(['id', 'name', 'email'])->from('users')->where('status' => 'active')->limit(4);

echo $queryBuilder->getHTML($records);
```

##### Output example 1

<table style="border-collapse:collapse;empty-cells:show">
  <tbody><tr>
    <th style="border-width:1px;border-style:solid;background-color:navy;color:white">id</th>
    <th style="border-width:1px;border-style:solid;background-color:navy;color:white">name</th>
    <th style="border-width:1px;border-style:solid;background-color:navy;color:white">email</th>
  </tr>
  <tr>
    <td style="border-width:1px;border-style:solid">2</td>
    <td style="border-width:1px;border-style:solid">Dur</td>
    <td style="border-width:1px;border-style:solid">dstiggers1@icio.us</td>
  </tr>
  <tr>
    <td style="border-width:1px;border-style:solid">3</td>
    <td style="border-width:1px;border-style:solid">Darsie</td>
    <td style="border-width:1px;border-style:solid">dohogertie2@pcworld.com</td>
  </tr>
  <tr>
    <td style="border-width:1px;border-style:solid">4</td>
    <td style="border-width:1px;border-style:solid">Rutter</td>
    <td style="border-width:1px;border-style:solid">rdonoghue3@house.gov</td>
  </tr>
  <tr>
    <td style="border-width:1px;border-style:solid">5</td>
    <td style="border-width:1px;border-style:solid">Carlota</td>
    <td style="border-width:1px;border-style:solid">ctipper4@jigsy.com</td>
  </tr>
</tbody></table>

{{< heading level="4" heading="Add styling" class="mt-5" small="Db::getHTML()" >}}

```php
$queryBuilder->select(['id', 'name', 'email'])->from('users')->where('status' => 'active')->limit(4);

echo $queryBuilder->getHTML($result, false, 'class=table table-striped, id=my-table', 'class=p-4 text-bg-dark', 'class=p-2');
```

<table class="table table-striped" id="my-table">
  <tbody><tr>
    <th class="p-4 text-bg-dark">id</th>
    <th class="p-4 text-bg-dark">name</th>
    <th class="p-4 text-bg-dark">email</th>
  </tr>
  <tr>
    <td class="p-2">2</td>
    <td class="p-2">Dur</td>
    <td class="p-2">dstiggers1@icio.us</td>
  </tr>
  <tr>
    <td class="p-2">3</td>
    <td class="p-2">Darsie</td>
    <td class="p-2">dohogertie2@pcworld.com</td>
  </tr>
  <tr>
    <td class="p-2">4</td>
    <td class="p-2">Rutter</td>
    <td class="p-2">rdonoghue3@house.gov</td>
  </tr>
  <tr>
    <td class="p-2">5</td>
    <td class="p-2">Carlota</td>
    <td class="p-2">ctipper4@jigsy.com</td>
  </tr>
</tbody></table>

</article>

{{< separator >}}

<article>

### Adding Parameters

#### QueryBuilder::distinct

The `distinct` method is used to specify that the query should return distinct results. It requires no argument.

```php
public function distinct() : self
```

#### QueryBuilder::groupBy {.mt-5}

The `groupBy` method is used to group the results by one or more columns.

```php
public function groupBy(string $column) : self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $column | string | The GROUP BY clause. | <pre class="{{< param "arguments_code_class">}}">'name'<br>'name, status'</pre> |

#### QueryBuilder::limit {.mt-5}

The `limit` method is used to limit the number of results returned by the query.

```php
public function limit(int $limit) : self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $limit | int | The LIMIT clause. | <pre class="{{< param "arguments_code_class">}}"> 10<br> '10, 20' </pre> |

#### QueryBuilder::orderBy {.mt-5}

The `orderBy` method is used to sort the results by one or more columns.

```php
public function orderBy(string $orderBy) : self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $orderBy | string | The ORDER BY clause. | <pre class="{{< param "arguments_code_class">}}"> 'name'<br> 'email DESC' </pre> |

#### QueryBuilder::parameters {.mt-5}

The `parameters` method is an alternative to the other parameter methods. It allows you to pass several parameters in a single method call.

```php
public function parameters(array $parameters) : self
```

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $parameters | array | An associative array of parameters. | <pre class="{{< param "arguments_code_class">}}"> ['distinct' => true, 'orderBy' => 'name ASC']<br> ['groupBy' => 'role', 'limit' => 20] </pre> |

{{< heading level="4" heading="QueryBuilder::select() examples with parameters" class="mt-5" small="QueryBuilder::select()" >}}

```php
// select distinct
$queryBuilder->select(['name'])->distinct()->from('users')->execute();

// orderBy + limit
$queryBuilder->select(['id, name'])->from('users')->orderBy('name')->limit(20)->execute();

// orderBy direction + limit start/end
$queryBuilder->select(['id, name'])->from('users')->orderBy('name DESC')->limit('20, 40')->execute();

// using the parameters method to group the parameters in a single method call
$queryBuilder->select(['id', 'name', 'email'])->from('users')->where(['status' => 'active'])->parameters(['limit' => 10, 'orderBy' => 'name ASC'])->execute();

// fetch the results
while ($record = $queryBuilder->fetch()) {
    echo $record->id . ', ' . $record->name . ', ' . $record->email;
}
```

</article>
