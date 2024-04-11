---
title: "Query Builder - Transaction Management"
linkTitle: "Transaction Management"
date: 2024-03-29T08:58:18+01:00
draft: false
description: "Efficiently manage your database transactions with QueryBuilder. Learn how to initiate, commit, and rollback transactions for precise control."
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

This page provides a practical guide with code samples for managing transactions using the `QueryBuilder` class in the PowerLitePdo library. The following methods are covered:

- [QueryBuilder::transactionBegin](/docs/{{< param "doc_version">}}/querybuilder-transaction-management/#transactionbegin)
- [QueryBuilder::transactionCommit](/docs/{{< param "doc_version">}}/querybuilder-transaction-management/#transactioncommit)
- [QueryBuilder::transactionRollback](/docs/{{< param "doc_version">}}/querybuilder-transaction-management/#transactionrollback)

<!--more-->

## Loading the QueryBuilder Class

Before you can use the `QueryBuilder` class, you need to load it within the Dependency Injection (DI) container.

```php
use Migliori\PowerLitePdo\Query\QueryBuilder;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$queryBuilder = $container->get(QueryBuilder::class);
```

## transactionBegin {.mt-5}

This method starts a new database transaction.

### Method Signature ### {#transactionBeginMethodSignature .mt-5}

```php
public function transactionBegin(): bool
```

### Examples ### {#transactionBeginExamples .mt-5}

```php
$queryBuilder->transactionBegin();
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
$queryBuilder->transactionBegin();

// Perform some database operations...

$queryBuilder->transactionCommit(); // Commit the transaction
```

## Db::transactionRollback

This method rolls back the current database transaction.

### Method Signature ### {#transactionRollbackMethodSignature .mt-5}

```php
public function transactionRollback(): bool
```

### Examples ### {#transactionRollbackExamples .mt-5}

```php
$queryBuilder->transactionBegin();

try {
    // Perform some database operations...

    $queryBuilder->transactionCommit(); // Commit the transaction
} catch (\Exception $e) {
    $queryBuilder->transactionRollback(); // Rollback the transaction in case of an error
}
```
