---
title: "Db - Database Structure Information"
linkTitle: "Database Structure Information"
date: 2024-03-29T09:02:14+01:00
draft: false
description: "Get detailed insights into the database structure with PowerLite PDO"
noindex: false
comments: false
nav_weight: 700
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

This page provides a comprehensive guide on how to use the `Db` class to retrieve information about the database structure. It includes practical code samples for each method.

<!--more-->

- [Db::getTables](/docs/{{< param "doc_version">}}/db-database-structure-information/#dbgettables)
- [Db::getColumns](/docs/{{< param "doc_version">}}/db-database-structure-information/#dbgetcolumns)
- [Db::getColumnsNames](/docs/{{< param "doc_version">}}/db-database-structure-information/#dbgetcolumnsnames)

## Loading the Db class

To use the `Db` class, you first need to load it within the Dependency Injection (DI) container.

```php
use Migliori\PowerLitePdo\Db;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$db = $container->get(Db::class);
```

{{< separator >}}

<article>

## Db::getTables() {.mt-5}

This method returns an array of table names from the database if successful, otherwise it returns false.

### Method Signature ### {#getTablesMethodSignature .mt-5}

```php
public function getTables(?string $debug = null): mixed
```

### Arguments Summary ### {#getTablesArgumentsSummary .mt-5}

| Argument | Type | Description | Example |
| --- | --- | --- | --- |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#getTablesExamples .mt-5}

```php
$tables = $db->getTables();
if ($tables !== false) {
    foreach ($tables as $table) {
        echo "Table: $table\n";
    }
} else {
    echo "Failed to retrieve tables.\n";
}
```

</article>

{{< separator >}}

<article>

## Db::getColumns() {.mt-5}

This method retrieves information about the columns in a given table.

### Method Signature ### {#getColumnsMethodSignature .mt-5}

```php
public function getColumns(string $table, int $fetchParameters = PDO::FETCH_OBJ, $debug = false): mixed
```

### Arguments Summary ### {#getColumnsArgumentsSummary .mt-5}

| Argument | Type | Description | Example |
| --- | --- | --- | --- |
| $table | string | The name of the table | <pre class="{{< param "arguments_code_class">}}">users<br>orders<br>products</pre> |
| $fetchParameters | ?int | The fetch style. Defaults to `PDO::FETCH_OBJ` | <pre class="{{< param "arguments_code_class">}}">PDO::FETCH_OBJ<br>PDO::FETCH_ASSOC</pre> |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#getColumnsExamples .mt-5}

```php
$columns = $db->getColumns('users');
var_dump($columns);
```

This will output the detailed column information for the 'users' table. For instance:

```php
array (size=5)
  0 =>
    object(stdClass)[33]
      public 'Field' => string 'id' (length=2)
      public 'Type' => string 'int(11) unsigned' (length=16)
      public 'Null' => string 'NO' (length=2)
      public 'Key' => string 'PRI' (length=3)
      public 'Default' => null
      public 'Extra' => string 'auto_increment' (length=14)
  1 =>
    // ... etc
```

</article>

{{< separator >}}

<article>

## Db::getColumnsNames() {.mt-5}

This method returns the column names of the target table.

### Method Signature ### {#getColumnsNamesMethodSignature .mt-5}

```php
public function getColumnsNames(string $table, ?string $debug = null): mixed
```

### Arguments Summary ### {#getColumnsNamesArgumentsSummary .mt-5}

| Argument | Type | Description | Example |
| --- | --- | --- | --- |
| $table | string | The name of the table | <pre class="{{< param "arguments_code_class">}}">users<br>orders<br>products</pre> |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#getColumnsNamesExamples .mt-5}

```php
$db = new Db();
$columnNames = $db->getColumnsNames('users');

var_dump($columnNames);
```

In this example, we are fetching the column names of the 'users' table.

</article>
