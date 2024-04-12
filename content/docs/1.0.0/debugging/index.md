---
title: "Debugging in PowerLitePdo"
linkTitle: "Debugging"
date: 2024-03-31T10:08:31+02:00
draft: false
description: "The Debugging section of PowerLite PDO documentation is your resource for understanding and implementing effective debugging techniques."
noindex: false
comments: false
nav_weight: 700
nav_icon:
  vendor: fas
  name: bug
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

## Introduction

PowerLitePdo provides a robust debugging system that allows developers to track and understand the execution of SQL queries. The debugging system is built around two contexts: a global context and a local context. The local context is attached to method calls like `select()`, `query()`, `insert()`, `update()`, `delete()`, etc., and takes precedence over the global context.

<!--more-->

The debugging mode can be set to three possible values: `true`, `false`, or `'silent'`.

- `true`: The class will display detailed error messages.
- `false`: The class will not display any error messages.
- `'silent'`: The class will register all error messages, which can be retrieved using the `getDebug()` method.

**When the `debug` mode is enabled, the `insert`, `update`, and `delete` statements are not executed.**

**Instead, the system internally uses a transaction to retrieve the debug information and then rolls back the transaction.**

{{< separator >}}

<article>

## Debugging with the Db Class

The `Db` class uses the `setDebug()` method to set the global debug mode. The local debug mode can be enabled using the `@param bool|string $debug` argument on method calls when available.

Here is the `setDebug()` method from the `Db` class:

```php
public function setDebug($debug): self
```

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $debug | bool\|string | The debug mode to set. Can be `true`, `false`, or `'silent'`. | <pre class="{{< param "arguments_code_class">}}">true<br>false<br>'silent'</pre> |

{{< heading level="3" heading="Example of using the `setDebug()` method with Db" class="mt-5" small="Db::setDebug()" >}}

```php
// Enable the Debug mode globally
$db->setDebug(true);

$db->update(...); // Debug mode is enabled, the page will display the information and the update will not be executed.

$db->update(..., false); // Debug mode is disabled locally, the update will be executed and no debug information will be displayed.
```

</article>

{{< separator >}}

<article>

## Debugging with the QueryBuilder Class

The `QueryBuilder` class uses the `setDebug()` and `debugOnce()` methods to set the global and local debug modes respectively.

Here is the `setDebug()` method from the `QueryBuilder` class:

```php
public function setDebug($debug): self
```

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $debug | bool\|string | The debug mode to set. Can be `true`, `false`, or `'silent'`. | <pre class="{{< param "arguments_code_class">}}">true<br>false<br>'silent'</pre> |

{{< heading level="3" heading="Example of using the `setDebug()` method with the QueryBuilder" class="mt-5" small="QueryBuilder::setDebug()" >}}

```php
// Enable the Debug mode globally
$queryBuilder->setDebug(true);
```

Here is the `debugOnce()` method from the `QueryBuilder` class:

```php
public function debugOnce($debug): self
```

| Argument | Type | Description | Examples |
| --- | --- | --- | --- |
| $debug | bool\|string | The debug mode to set for a single query. Can be `true`, `false`, or `'silent'`. | <pre class="{{< param "arguments_code_class">}}">true<br>false<br>'silent'</pre> |

{{< heading level="3" heading="Example of using the QueryBuilder's `debugOnce()` method" class="mt-5" small="QueryBuilder::debugOnce()" >}}

```php
// Enable the Debug mode locally
$queryBuilder->insert($table, $values)->debugOnce(true);
```

Both the `Db` and `QueryBuilder` classes have a `getDebug()` method that returns the view of the debugging data, which includes the prepared SQL, the parameters, the final SQL, and other information.
</article>
