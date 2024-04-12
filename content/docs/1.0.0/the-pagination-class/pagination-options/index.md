---
title: "Pagination - Options"
linkTitle: "Pagination Options"
date: 2024-03-29T12:00:36+01:00
draft: false
description: "Learn how to customize your pagination with various options."
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
#         vendor: fas
#         name: book
#         color: '#e24d0e'
---

The PaginationOptions class and the Pagination::setOptions() method provide a way to customize the behavior and appearance of pagination in your application. By setting these options, you can control aspects such as the CSS classes applied to various elements of the pagination, the markup used for navigation buttons, the number of pages displayed in the navigation, and more.

<!--more-->

## Pagination::setOptions()

This method is used to set the options for pagination. Here is the method signature:

```php
public function setOptions(array $options): void
```

### Arguments

| Argument | Type | Description | Example |
| --- | --- | --- | --- |
| $options | `array<string, bool\|string>` | An array of options for pagination. | <pre class="{{< param "arguments_code_class">}}">$options = [<br>    'activeClass' => 'active-page',<br>    'navLength' => 5<br>];<br>$pagination->setOptions($options);</pre> |

## PaginationOptions

The PaginationOptions class represents the options for pagination. Here are the properties of this class:

- `$activeClass`: The CSS class for the active page. Default is 'active'.
- `$disabledClass`: The CSS class for the disabled page. Default is 'disabled'.
- `$paginationClass`: The CSS class for the pagination container. Default is 'pagination pagination-flat'.
- `$firstMarkup`: The markup for the "First" button. Default is '<i class="fas fa-angle-double-left"></i>'.
- `$previousMarkup`: The markup for the "Previous" button. Default is '<i class="fas fa-angle-left"></i>'.
- `$nextMarkup`: The markup for the "Next" button. Default is '<i class="fas fa-angle-right"></i>'.
- `$lastMarkup`: The markup for the "Last" button. Default is '<i class="fas fa-angle-double-right"></i>'.
- `$navLength`: The number of pages to display in the navigation. Default is 2.
- `$querystring`: The query string to append to the pagination links. E.g.`: 'p' for page. Default is 'p'.
- `$rewriteLinks`: Indicates whether to rewrite the pagination links. Default is false.
- `$rewriteTransition`: The transition string used for rewriting the pagination links. Default is '&'.
- `$rewriteExtension`: The file extension used for rewriting the pagination links. Default is ''.

## Examples

Here are some examples of how to use the Pagination::setOptions() method and the PaginationOptions class:

```php
// Create a new Pagination object
use Migliori\PowerLitePdo\Pagination;

$container = require_once __DIR__ . '/../src/bootstrap.php';
$pagination = $container->get(Pagination::class);

// Set options
$options = [
    'activeClass' => 'active-page',
    'navLength' => 5,
    'rewriteLinks' => true,
    'rewriteTransition' => '/',
    'rewriteExtension' => '.html'
];
$pagination->setOptions($options);
```

In this example, we're setting the CSS class for the active page to 'active-page', displaying 5 pages in the navigation, and rewriting the pagination links to use '/' as the transition string and '.html' as the file extension.
