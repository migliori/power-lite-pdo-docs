---
title: "Getting Started"
version: "v1.0"
series:
  - v1.0
nav_weight: 200
nav_icon:
  vendor: fas
  name: circle-play
  color: '#548289'
---

## Setup the Database Connection

To set up your database connection, you will need to modify the `vendor/migliori/power-lite-pdo/src/connection.php` file. This file contains the configuration for the database connection using PHP's PDO (PHP Data Objects).

Here are the steps to set up your database connection:

1. **Choose your Database Driver**: The PDO extension supports multiple databases. You can choose the one that suits your needs. The driver name should be set as the value of the `PDO_DRIVER` constant. For example, if you are using MySQL, the line should look like this:

    ```php
    define('PDO_DRIVER', 'mysql');
    ```

2. **Configure your Local Server Settings**: If you are running your application on a local server for development purposes, you will need to set the database host, name, user, and password. These are defined as constants in the `connection.php` file. Here is an example of how to set these values:

    ```php
    define('DB_HOST', 'localhost'); // Database host
    define('DB_NAME', 'sampledatabase'); // Database name
    define('DB_USER', 'root'); // Database user
    define('DB_PASS', 'Mysql'); // Database password
    ```

3. **Configure your Production Server Settings**: If you are deploying your application to a production server, you will need to set the database host, name, user, and password for the production environment. These are also defined as constants in the `connection.php` file. Here is an example of how to set these values:

    ```php
    define('DB_HOST', 'production-db_host'); // Database host
    define('DB_NAME', 'production-db_name'); // Database name
    define('DB_USER', 'production-db_user'); // Database user
    define('DB_PASS', 'production-db_password'); // Database password
    ```

Replace `'localhost'`, `'sampledatabase'`, `'root'`, `'Mysql'`, `'production-db_host'`, `'production-db_name'`, `'production-db_user'`, and `'production-db_password'` with your actual database host, name, user, and password respectively for both local and production environments.

The program will automatically detect if it's running on a local or production server and use the appropriate settings accordingly.

## Security

To optimize the security of your connection parameters, please refer to the [Security](/docs/{{< param "doc_version" >}}/security) section.

## Choosing Your Database Interaction Style

In PowerLite PDO, you have two primary ways to interact with the database: the `Db` class and the `QueryBuilder`. The `Db` class offers procedural methods for database operations, while the `QueryBuilder` provides a fluent interface for building SQL queries. The choice between these two depends on your personal preference and coding style.

## Database, QueryBuilder and Pagination

The `Database` and the `QueryBuilder` both provide convenient ways to interact with the database and fetch results. However, while the `Database` employs a procedural style through the use of methods, the `QueryBuilder` utilizes fluent methods. Choose the one that best aligns with your preferred coding style.

### Initializing Db Instance

To get a `Db` instance, you would use the following code:

```php
use Migliori\PowerLitePdo\Db;

$container = require_once __DIR__ . '/vendor/migliori/power-lite-pdo/src/bootstrap.php';

$db = $container->get(Db::class);
```

This will return an instance of the `Db` class, which you can use to interact with the database.

### Initializing QueryBuilder Instance

To get a `QueryBuilder` instance, you would use the following code:

```php
use Migliori\PowerLitePdo\Query\QueryBuilder;

$container = require_once __DIR__ . '/vendor/migliori/power-lite-pdo/src/bootstrap.php';

$queryBuilder = $container->get(QueryBuilder::class);
```

This will return an instance of the `QueryBuilder` class, which you can use to build SQL queries in a safe and efficient manner.

### Initializing Pagination Instance

To get a `Pagination` instance, you would use the following code:

```php
use Migliori\PowerLitePdo\Pagination;

$container = require_once __DIR__ . '/vendor/migliori/power-lite-pdo/src/bootstrap.php';

$pagination = $container->get(Pagination::class);
```

This will return an instance of the `Pagination` class, which you can use to paginate query results.

The DI container ensures that each instance is properly configured with its dependencies.
