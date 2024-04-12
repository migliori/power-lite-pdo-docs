---
title: "Db - Data Fetching and Conversion"
linkTitle: "Data Fetching and Conversion"
date: 2024-03-29T08:46:25+01:00
draft: false
description: "Get started with data fetching and conversion in PowerLite PDO. Our comprehensive guide covers all the essentials for manipulating data effectively."
noindex: false
comments: false
nav_weight: 500
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

This page provides a comprehensive guide on how to use the Db class for data fetching and conversion. The following methods are covered:

- [Db::fetch](/docs/{{< param "doc_version">}}/db-data-fetching-and-conversion/#dbfetch)
- [Db::fetchAll](/docs/{{< param "doc_version">}}/db-data-fetching-and-conversion/#dbfetchall)
- [Db::convertToSimpleArray](/docs/{{< param "doc_version">}}/db-data-fetching-and-conversion/#dbconverttosimplearray)
- [Db::getHTML](/docs/{{< param "doc_version">}}/db-data-fetching-and-conversion/#dbgethtml)

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

## Db::fetch() {.mt-5}

Fetches the next row from a result set and returns it according to the $fetchParameters format.

### Method Signature ### {#fetchMethodSignature .mt-5}

```php
public function fetch(int $fetchParameters = PDO::FETCH_OBJ): mixed
```

### Arguments Summary ### {#fetchArgumentsSummary .mt-5}

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $fetchParameters | ?int | The PDO Fetch mode | <pre class="{{< param "arguments_code_class">}}">PDO::FETCH_OBJ<br>PDO::FETCH_ASSOC</pre> |

### Examples ### {#fetchExamples .mt-5}

{{< heading level="4" heading="Simple Use Case" small="Db::fetch()" >}}

```php
$db->query("SELECT * FROM users");
while ($row = $db->fetch(PDO::FETCH_ASSOC)) {
    echo $row['name'];
}
```

In this example, we are fetching rows from the "users" table as associative arrays.

{{< heading level="4" heading="Using Default Fetch Mode" class="mt-5" small="Db::fetch()" >}}

```php
$db->query("SELECT * FROM users");
while ($row = $db->fetch()) {
    echo $row->name;
}
```

In this example, we are fetching rows from the "products" table using the default fetch mode (PDO::FETCH_OBJ), which returns rows as objects.

</article>

{{< separator >}}

<article>

## Db::fetchAll() {.mt-5}

Fetches all rows from a result set and return them according to the $fetchParameters format.

### Method Signature ### {#fetchAllMethodSignature .mt-5}

```php
public function fetchAll(int $fetchParameters = PDO::FETCH_OBJ) : mixed
```

### Arguments Summary ### {#fetchAllArgumentsSummary .mt-5}

| Argument Name | Argument Type | Description | Examples |
| --- | --- | --- | --- |
| $fetchParameters | ?int | The PDO fetch style record options | <pre class="{{< param "arguments_code_class">}}">PDO::FETCH_OBJ<br>PDO::FETCH_ASSOC</pre> |

### Examples ### {#fetchAllExamples .mt-5}

{{< heading level="4" heading="fetchAll" class="mt-5" small="Db::fetchAll()" >}}

```php
$db->query("SELECT * FROM users");

// fetch all rows from the result set and return them as objects.
$result = $db->fetchAll(PDO::FETCH_OBJ);

// fetch all rows from the result set and return them as associative arrays.
$result = $db->fetchAll(PDO::FETCH_ASSOC);
```

</article>

{{< separator >}}

<article>

## Db::convertToSimpleArray() {.mt-5}

```php
public function convertToSimpleArray(mixed $array, string $value_field, ?string $key_field = null): array<string|int, mixed>
```

The `Db::convertToSimpleArray()` method converts a Query() or Select() array of records into a simple array using only one column or an associative array using another column as a key.

### Method Signature ### {#convertToSimpleArrayMethodSignature .mt-5}

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $array | mixed | An array of records from a Query() or Select() operation. | <pre class="{{< param "arguments_code_class">}}">[['id' => 1, 'name' => 'John'], ['id' => 2, 'name' => 'Jane']]<br>[['id' => 3, 'name' => 'Doe']]</pre> |
| $value_field | string | The name of the column to use for the values of the resulting array. | <pre class="{{< param "arguments_code_class">}}">'name'</pre> |
| $key_field | ?string | The name of the column to use for the keys of the resulting array. If not provided, the resulting array will be indexed by integers. | <pre class="{{< param "arguments_code_class">}}">'id'</pre> |

### Examples ### {#convertToSimpleArrayExamples .mt-5}

{{< heading level="4" heading="Convert to a simple array" small="Db::convertToSimpleArray()" >}}

```php
$db->select('users', ['id', 'name']);

// fetch all rows from the result set and return them as associative arrays.
$result = $db->fetchAll(PDO::FETCH_ASSOC);

// convert the result to an indexed array. E.g.: ["name,", "name2", ...]
$result = $db->convertToSimpleArray($result, 'name');

var_dump($result);

/* will output:
array (size=1000)
    0 => string 'Royall'
    1 => string 'Dur'
    2 => string 'Darsie'
    // ...
*/
```

{{< heading level="4" heading="Convert to an associative array" small="Db::convertToSimpleArray()" >}}

```php
$query = $db->select('users', ['name', 'email']);

// fetch all rows from the result set and return them as associative arrays.
$result = $db->fetchAll(PDO::FETCH_ASSOC);

// convert the result to an associative array. E.g.: ["name" => "email", ...]
// note that the arguments order is 'value', 'key', because the key is optional
$result = $db->convertToSimpleArray($result, 'email', 'name');

var_dump($result);

/* will output:
array
    'Royall' => string 'rcostanza0@etsy.com'
    'Dur' => string 'dsprouls3y@clickbank.net'
    'Darsie' => string 'dohogertie2@pcworld.com'
    // ...
*/
```

</article>

{{< separator >}}

<article>

## Db::getHTML() {.mt-5}

The `Db::getHTML` method is used to convert a records set into an HTML table.

### Method Signature ### {#getHTMLMethodSignature .mt-5}

```php
public function getHTML(
    array $records,
    bool $showCount = true,
    ?string $tableAttr = null,
    ?string $thAttr = null,
    ?string $tdAttr = null
): string
```

### Arguments Summary ### {#getHTMLArgumentsSummary .mt-5}

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $records | array | The records set - can be an array or array of objects according to the fetch parameters. | <pre class="{{< param "arguments_code_class">}}">[['name' => 'John', 'age' => 30], ['name' => 'Jane', 'age' => 25]]<br>[new User('John', 30), new User('Jane', 25)]</pre> |
| $showCount | ?bool | True if you want to show the row count, false if you do not want to show the count. Default is true. | <pre class="{{< param "arguments_code_class">}}">true<br>false</pre> |
| $tableAttr | ?string | Comma separated attributes for the table. | <pre class="{{< param "arguments_code_class">}}">'class=my-class, style=color:#222'</pre> |
| $thAttr | ?string | Comma separated attributes for the header row. | <pre class="{{< param "arguments_code_class">}}">'class=my-class, style=font-weight:bold'</pre> |
| $tdAttr | ?string | Comma separated attributes for the cells. | <pre class="{{< param "arguments_code_class">}}">'class=my-class, style=font-weight:normal'</pre> |

The method returns a string containing an HTML table with all records listed.

### Examples ### {#getHTMLExamples .mt-5}

{{< heading level="4" heading="Basic example" small="Db::getHTML()" >}}

```php
$db->select('users', ['id', 'name', 'email'], ['status' => 'active'], ['limit' => 4]);

echo $db->getHTML($records);
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
$db->select('users', ['id', 'name', 'email'], ['status' => 'active'], ['limit' => 4]);

echo $db->getHTML($result, false, 'class=table table-striped, id=my-table', 'class=p-4 text-bg-dark', 'class=p-2');
```

##### Output example 2

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
