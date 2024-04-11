---
title: "Db - SQL Query Execution"
linkTitle: "SQL Query Execution"
date: 2024-03-29T07:47:15+01:00
draft: false
description: "Get started with SQL query execution in PowerLite PDO. Our comprehensive guide covers everything you need to know to run SQL queries effectively."
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

This page provides a comprehensive guide on how to execute SQL queries using the `Db` class in your project. We will cover the following methods:

- [Db::query](/docs/{{< param "doc_version">}}/db-sql-query-execution/#query)
- [Db::queryRow](/docs/{{< param "doc_version">}}/db-sql-query-execution/#queryrow)
- [Db::queryValue](/docs/{{< param "doc_version">}}/db-sql-query-execution/#queryvalue)
- [Db::numRows](/docs/{{< param "doc_version">}}/db-sql-query-execution/#numrows)

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

## query() {#query.mt-5}

The `Db::query()` method is used to execute SQL queries. It takes a SQL statement as a string, an optional array of placeholders, and an optional debug mode.

### Method Signature ### {#queryMethodSignature .mt-5}

```php
public function query(
    string $sql,
    array $placeholders = [],
    bool|string $debug = false
): bool
```

### Arguments Summary ### {#queryArgumentsSummary .mt-5}

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $sql | string | The SQL query to execute. | <pre class="{{< param "arguments_code_class">}}">SELECT * FROM users WHERE id = :id<br>INSERT INTO users (name, email) VALUES (:name, :email)</pre> |
| $placeholders | ?array | An indexed or associative array to store the placeholders used in the query. | <pre class="{{< param "arguments_code_class">}}">['id' => 1]<br>['name' => 'John', 'email' => 'john@example.com']<br>['John', 'john@example.com']</pre> |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#queryExamples .mt-5}

{{< heading level="4" heading="SELECT query" small="Db::query()" >}}

```php
// SQL statement using named parameters. You can use this approach to specify values by name.
$sql = "SELECT * FROM users WHERE id = :id";
$placeholders = ['id' => 1];

// SQL statement using positional parameters. This approach allows you to specify values by their position.
$sql = "SELECT * FROM users WHERE id = ?";
$placeholders = [1];

$db->query($sql, $placeholders);

while ($row = $db->fetch()) {
    echo $row->name;
}
```

{{< heading level="4" heading="INSERT statement" class="mt-5" small="Db::query()" >}}

```php
// SQL statement using named parameters. You can use this approach to specify values by name.
$sql = "INSERT INTO users (id, name, email, profiles_id, status) VALUES (NULL, :name, :email, :profiles_id, :status)";
$parameters = ['name' => 'John', 'email' => 'john@example.com', 'profiles_id' => 1, 'status' => 'active'];

// SQL statement using positional parameters. This approach allows you to specify values by their position.
$sql = "INSERT INTO users (id, name, email, profiles_id, status) VALUES (NULL, ?, ?, ?, ?)";
$parameters = ['John', 'john@example.com', 1, 'active'];

// Send the query and retrieve the number of affected rows
$affectedRows = $db->query($sql, $placeholders);

// Get the last insert id
$lastInsertId = $db->getLastInsertId();
```

{{< heading level="4" heading="UPDATE statement" class="mt-5" small="Db::query()" >}}

```php
// SQL statement using named parameters. You can use this approach to specify values by name.
$sql = "UPDATE users SET name = :name WHERE id = :id";
$placeholders = ['name' => 'Jane', 'id' => $lastInsertId];

// SQL statement using positional parameters. This approach allows you to specify values by their position.
$sql = "UPDATE users SET name = ? WHERE id = ?";
$placeholders = ['Jane', $lastInsertId];

// Send the query and retrieve the number of affected rows
$affectedRows = $db->query($sql, $placeholders);
```

{{< heading level="4" heading="DELETE statement" class="mt-5" small="Db::query()" >}}

```php
// SQL statement using named parameters. You can use this approach to specify values by name.
$sql = "DELETE FROM users WHERE id = :id";
$placeholders = ['id' => $lastInsertId];

// SQL statement using positional parameters. This approach allows you to specify values by their position.
$sql = "DELETE FROM users WHERE id = ?";
$placeholders = [$lastInsertId];

// Send the query and retrieve the number of affected rows
$affectedRows = $db->query($sql, $placeholders);
```

</article>

{{< separator >}}

<article>

## Db::queryRow() {#queryrow .mt-5}

The `Db::queryRow` method executes a SQL query using PDO and returns one row.

### Method Signature ### {#queryRowMethodSignature .mt-5}

```php
public function queryRow(
    string $sql,
    array $placeholders = [],
    $fetchParameters = PDO::FETCH_OBJ,
    bool|string $debug = false
)
```

### Arguments Summary ### {#queryRowArgumentsSummary .mt-5}

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $sql | string | The SQL query to execute. | <pre class="{{< param "arguments_code_class">}}">SELECT *FROM customers WHERE country = :country<br>SELECT* FROM customers WHERE country = ?</pre> |
| $placeholders | ?array | An associative array of placeholders to substitute in the SQL query. | <pre class="{{< param "arguments_code_class">}}">['country' => 'Indonesia']<br>['Indonesia']</pre> |
| $fetchParameters | ?int | The PDO fetch style. | <pre class="{{< param "arguments_code_class">}}">PDO::FETCH_OBJ<br>PDO::FETCH_ASSOC</pre> |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#queryRowExamples .mt-5}

{{< heading level="4" heading="Query a single ROW" small="Db::queryRow()" >}}

```php
// SQL statement using named parameters. You can use this approach to specify values by name.
$sql = "SELECT * FROM customers WHERE country = :country";
$placeholders = ['country' => 'Indonesia'];

// SQL statement using positional parameters. This approach allows you to specify values by their position.
$sql = "SELECT * FROM customers WHERE country = ?";
$placeholders = ['Indonesia'];

// Send the query and get the result
$result = $db->queryRow($sql, $placeholders, PDO::FETCH_OBJ);
if ($result) {
    echo "ID: " . $result->id;
    echo "First Name: " . $result->first_name;
}
```

In both examples, the `queryRow` method is used to execute a SQL query that returns a single Row. The `$params` argument is used to safely bind parameters in the SQL query, preventing SQL injection attacks.

</article>

{{< separator >}}

<article>

## Db::queryValue() {#queryValue.mt-5}

### Method Signature ### {#queryValueMethodSignature .mt-5}

```php
public function queryValue(
    string $sql,
    array $placeholders = [],
    bool|string $debug = false
)
```

The `Db::queryValue` method executes a SQL query using PDO and returns a single value only.

### Arguments Summary ### {#queryValueArgumentsSummary .mt-5}

| Argument | Type | Description | Example |
|----------|------|-------------|---------|
| $query   | string | The SQL query to execute. | <pre class="{{< param "arguments_code_class">}}">SELECT name FROM users WHERE id = :id</pre> |
| $params  | ?array | An optional array of parameters to bind in the SQL query. | <pre class="{{< param "arguments_code_class">}}">['id' => 1]</pre> |
| $debug | {{< arguments/debug type="true" >}} | {{< arguments/debug description="true" >}} | {{< arguments/debug examples="true" >}} |

### Examples ### {#queryValueExamples .mt-5}

{{< heading level="4" heading="Query a value" small="Db::queryValue()" >}}

```php
// SQL statement using named parameters. You can use this approach to specify values by name.
$query = "SELECT name FROM users WHERE id = :id";
$params = [':id' => 1];

// SQL statement using positional parameters. This approach allows you to specify values by their position.
$query = "SELECT name FROM users WHERE id = ?";
$params = [1];

// Send the query and get the result
$result = $db->queryValue($query, $params);
echo $result;  // Outputs the name of the user with id 1
```

In both examples, the `queryValue` method is used to execute a SQL query that returns a single value. The `$params` argument is used to safely bind parameters in the SQL query, preventing SQL injection attacks.
</article>

{{< separator >}}

<article>

## numRows() {#numRows.mt-5}

The `Db::numRows` method is used to get the number of rows in the result set of the current query.

### Method Signature ### {#numRowsMethodSignature .mt-5}

```php
public function numRows(): int|false
```

The `Db::numRows` method does not take any arguments and returns either an integer representing the number of rows, or `false` on failure.

### Examples ### {#numRowsExamples .mt-5}

{{< heading level="4" heading="Num rows after select" small="Db::numRows()" >}}

```php
$db->query("SELECT * FROM users");
$result = $db->numRows();

echo $result; // Outputs the number of rows in the "users" table
```

</article>
