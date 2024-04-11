---
title: "Db - Transaction Management"
linkTitle: "Transaction Management"
date: 2024-03-29T08:58:18+01:00
draft: false
description: "Master Transaction Management with PowerLite PDO documentation. Understand how to commit, rollback, and manage your database transactions efficiently."
noindex: false
comments: false
nav_weight: 600
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

This page provides a practical guide with code samples for managing transactions using the `Db` class in the PowerLitePdo library. The following methods are covered:

- [Db::transactionBegin](/docs/{{< param "doc_version">}}/db-transaction-management/#transactionbegin)
- [Db::transactionCommit](/docs/{{< param "doc_version">}}/db-transaction-management/#transactioncommit)
- [Db::transactionRollback](/docs/{{< param "doc_version">}}/db-transaction-management/#transactionrollback)

<!--more-->

## Loading the Db Class

To use the `Db` class, you first need to load it within the Dependency Injection (DI) container. Here's how you can do it:

```php
$container['db'] = function ($container) {
    return new \Migliori\PowerLitePdo\Db($container['settings']['db']);
};
```

## transactionBegin {.mt-5}

This method starts a new database transaction.

### Method Signature ### {#transactionBeginMethodSignature .mt-5}

```php
public function transactionBegin(): bool
```

### Examples ### {#transactionBeginExamples .mt-5}

```php
$db->transactionBegin();
// Perform some database operations...
```

## Db::transactionCommit {.mt-5}

This method commits the current database transaction.

### Method Signature ### {#transactionCommitMethodSignature .mt-5}

```php
public function transactionCommit(): bool
```

### Examples ### {#transactionCommitExamples .mt-5}

```php
$db->transactionBegin();

// Perform some database operations...

$db->transactionCommit(); // Commit the transaction
```

## Db::transactionRollback

This method rolls back the current database transaction.

### Method Signature ### {#transactionRollbackMethodSignature .mt-5}

```php
public function transactionRollback(): bool
```

### Examples ### {#transactionRollbackExamples .mt-5}

```php
$db->transactionBegin();

try {
    // Perform some database operations...

    $db->transactionCommit(); // Commit the transaction
} catch (\Exception $e) {
    $db->transactionRollback(); // Rollback the transaction in case of an error
}
```
