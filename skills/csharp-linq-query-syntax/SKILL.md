---
name: csharp-linq-query-syntax
description: How to write a C# LINQ query expression (`from`...`select`) that ends in a method call like `Count()`, `ToList()`, or `First()`. Use whenever a query expression needs a trailing method call.
---

# C# LINQ query syntax

A query expression has no syntax of its own for calls like `Count` or `ToList`---don't bolt one on by parenthesizing the whole expression. Instead, pass the query expression as an argument to the equivalent `Enumerable`/`Queryable` static method.

Prefer:

```cs
var count = Queryable.Count(
    from b in db.Blogs
    where b.Name.Contains(".NET")
    select b);
```

Over:

```cs
var count = (from b in db.Blogs
             where b.Name.Contains(".NET")
             select b).Count();
```
