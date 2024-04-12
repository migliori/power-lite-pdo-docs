---
title: "Security"
# linkTitle:
draft: false
description: "PowerLite PDO Security Documentation: Your guide to secure database connectivity in PHP applications using PowerLite PDO."
noindex: false
# comments: false
nav_weight: 800
nav_icon:
  vendor: fas
  name: shield-halved
  color: '#548289'
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

The connection file, located at `src/connection.php`, contains important information for connecting to your database. It includes constants such as `DB_NAME`, `DB_PASS`, `DB_PORT`, and others. These constants are crucial for establishing a secure connection to your database.

While the connection file is already secure in its current location, there are additional measures that can be taken to enhance its security. These measures ensure that the sensitive information contained within the file is protected from unauthorized access.

## Enhancing the Security of the Connection File

### Relocating the Connection File

One method to enhance the security of the connection file is to relocate it out of the public document root. This adds an extra layer of protection by making the file inaccessible from the public web. To implement this, you need to modify the code in `src/bootstrap.php` to load the connection file from its new location.

```php
require_once '../path/to/connection.php';
```

### Using dotenv

An alternative way to enhance the security of your connection file is to use dotenv. dotenv is a zero-dependency module that loads environment variables from a `.env` file into `process.env`. This allows you to separate secrets from your source code. This is useful in a collaborative environment where you may not want to share your database login details with other developers.

To use dotenv, you need to install it via composer:

```sh
composer require vlucas/phpdotenv
```

Then, you can load the `.env` file in your `src/bootstrap.php`:

```php
$dotenv = Dotenv\Dotenv::createImmutable(__DIR__);
$dotenv->load();
```

And access your variables like so:

```php
$db = new Db(getenv('DB_NAME'), getenv('DB_PASS'));
```

Remember to add your `.env` file to your `.gitignore` to ensure it's not committed to your repository.

## Understanding the Connection Logic

The connection logic is handled by the `Db` class, which uses the constants defined in the connection file to establish a connection to the database. The `DriverManager` is responsible for managing the connection and the `QueryBuilder` is used to build and execute SQL queries.

By understanding how these components interact, you can better secure your application and protect your sensitive data.
