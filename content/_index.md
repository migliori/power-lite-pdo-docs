---
layout: 'landing'
images:
  - /images/powerlite-pdo-logo-horizontal.png
featured: true
---

![PowerLite PDO](/images/powerlite-pdo-logo-horizontal.png)

<div class="container">
    <div class="row">
        <div class="col-lg-12">
            <h1 class="fs-5 fw-semibold d-inline me-1">PowerLite PDO</h1>
            <p class="lead d-inline">is a powerful and lightweight PHP library designed to simplify the process of interacting with databases using PHP Data Objects (PDO). Primarily intended for developers who need a flexible, efficient, and easy-to-use tool for database operations.</p>
        </div>
    </div>
    <div class="row mt-5">
        <div class="col-lg-12">
            <h2>Core Components</h2>
            <p>The package is structured around three primary elements: <code>Db</code>, <code>QueryBuilder</code>, and <code>Pagination</code>.</p>
        </div>
    </div>
    <div class="row mt-3">
        <div class="col-lg-4">
            <h3>Db</h3>
            <p>The core of the package. It manages the database connection and provides a simple interface for executing queries and retrieving results. It also integrates with the <code>QueryBuilder</code> and <code>Pagination</code> classes to provide a seamless experience.</p>
        </div>
        <div class="col-lg-4">
            <h3>QueryBuilder</h3>
            <p>A powerful tool for building SQL queries in a programmatic and secure way. It abstracts the underlying SQL syntax and provides a fluent, chainable interface for constructing queries.</p>
        </div>
        <div class="col-lg-4">
            <h3>Pagination</h3>
            <p>Provides an easy way to handle pagination of results. It integrates with the <code>Db</code> and <code>QueryBuilder</code> classes to provide a simple, consistent API for paginating query results.</p>
        </div>
    </div>
    <div class="row mt-5">
        <div class="col-lg-12">
            <h2>Additional Components</h2>
            <p>In addition to these main classes, the package also includes a <code>DriverManager</code> class, which manages the database drivers for the PHP PDO DB Class. This class is used internally by the <code>Db</code> class to handle the specifics of different database drivers.</p>
        </div>
    </div>
    <div class="row mt-5">
        <div class="col-lg-12">
            <h2>Initialization</h2>
            <p>The package is initialized through the bootstrap.php file, which sets up the necessary configurations and initializes the <code>Db</code> class.</p>
        </div>
    </div>
    <div class="mt-5">
        <div class="col-lg-12">
            <div class="container">
                <div class="row">
                    <div class="col-lg-12">
                        <h2 class="mt-5">Discover More About PowerLite PDO</h2>
                        <p>PowerLite PDO is not just a tool, it's a comprehensive solution designed to make your database operations efficient and secure. It's user-friendly, yet robust and versatile, providing a solid base for all your database needs. It's capable of handling everything from simple tasks to complex queries and operations.</p>
                        <p>Whether you're working on a small personal project or a large enterprise application, PowerLite PDO is equipped with the features you need. But don't just take our word for it, explore more about PowerLite PDO in our documentation:</p>
                        <ul>
                            <li><a href="/docs/{{< param "doc_version" >}}/architecture-overview/">Architecture Overview</a></li>
                            <li><a href="/docs/{{< param "doc_version" >}}/getting-started/">Getting Started Guide</a></li>
                            <li><a href="/docs/{{< param "doc_version" >}}/db-introduction/">Introduction to Db Class</a></li>
                            <li><a href="/docs/{{< param "doc_version" >}}/query-builder-introduction/">Introduction to QueryBuilder</a></li>
                            <li><a href="/docs/{{< param "doc_version" >}}/pagination-select-and-paginate-results/">Select and Paginate Results with Pagination</a></li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
