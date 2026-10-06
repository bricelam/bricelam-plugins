---
name: csharp-primary-constructors
description: Don't use C# primary constructors on classes or structs. Use whenever writing a C# class or struct with constructor parameters, or when an IDE/analyzer suggests converting to a primary constructor.
---

# C# primary constructors

Don't use primary constructors on classes or structs. Parameter scope is too muddled: the parameters are captured implicitly, may be mutable, and read like fields without being declared as fields.

Declare fields (or properties) explicitly and assign them in a regular constructor.

Prefer:

```cs
public class BlogService
{
    private readonly BlogContext _db;

    public BlogService(BlogContext db)
    {
        _db = db;
    }
}
```

Over:

```cs
public class BlogService(BlogContext db)
{
}
```

Records may use their positional (primary) syntax, since it declares public properties rather than captured parameters.
