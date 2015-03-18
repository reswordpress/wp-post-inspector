# WP Post Inspector

Tools for interacting and inspecting WordPress post objects.

**I'm currently testing this, use at your own risk.**


- [Retrieving a post object](#retrieving-a-post-object)
- [Accessing post attributes](#accessing-post-attributes)
- [Traversing the post hierarchy](#traversing-a-post-hierarchy)

## Retrieving a post object

```php
// Get the current post object:
$post = Post::get();

// Get a specific post object by ID:
$post = Post::get(1);

// Get a specific post object by slug:
$post = Post::get('hello-world');
```

* * *

## Accessing post attributes
You may either use standard WP_Post attributes (as methods) or any of the shortcut methods built in to this class.

```php
// Display the current post title:
echo Post::title(); // "Hello world!"

// Display the title for a specific post:
$post = Post::get(1);

// Using a shortcut method:
echo $post->title(); // "Hello world!"

// Using a standard WP_Post attribute name:
echo $post->post_title(); // "Hello world!"

// Method chaining:
echo Post::get(1)->title(); // "Hello world!"
```

Attribute name          | Shortcut method
----------------------- | ---------------
ID                      | id
post_author             | author
post_date               | date
post_date_gmt           | gmt or dateGmt
post_content            | content
post_title              | title
post_excerpt            | excerpt
post_status             | status
comment_status          | commentStatus
ping_status             | pingStatus
post_password           | password
post_name               | name or slug
to_ping                 | toPing
pinged                  | pinged
post_modified           | modified
post_modified_gmt       | modifiedGmt
post_content_filtered   | contentFiltered
post_parent             | parent
guid                    | guid
menu_order              | menuOrder
post_type               | type
post_mime_type          | mimeType
comment_count           | commentCount
filter                  | filter
---

## Traversing the post hierarchy
You may traverse the post hierarchy using the `parent`, `top`, `ancestors`, `descendants`, and `siblings` methods:

```php
// Get the parent of the current post object:
$parent = Post::get()->parent();

// Accessing attributes on the parent object:
echo $parent->slug();

// Display the title of the top ancestor post object
echo Post::top()->title();

// The 'ancestors', 'descendants', and 'siblings' methods all return arrays of PostInspector objects:
$ancestors = Post::get()->ancestors();

foreach ($ancestors as $ancestor)
{
    var_dump($ancestor->title());
}

// Method chaining is possible:
$grandParent = Post::get()->parent()->parent();
$grandAunts = Post::get()->parent()->parent()->siblings();

```
