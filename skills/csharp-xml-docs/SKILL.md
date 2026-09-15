---
name: csharp-xml-docs
description: Conventions for writing C# XML documentation comments (`///`)---when to write them at all, which tags to use for code references and emphasis, and the standard wording for summaries, parameters, return values, properties, constructors, finalizers, and exceptions. Use whenever writing, reviewing, or editing `///` comments or tags like `<summary>`, `<param>`, `<returns>`, `<value>`, and `<exception>`, or whenever documenting a C# API---even if the user doesn't explicitly ask for "doc comments."
---

# C# XML doc comments

Conventions for XML documentation comments. Apply these by default; only deviate if the user says otherwise or the project already has an established, different convention.

## When to write them

Only write XML doc comments on public APIs. On non-public members they incur a compilation time and output size cost for no benefit---if a non-public member needs a non-obvious explanation, use a regular `//` comment instead.

## Tags

Prefer                    | Over
------------------------- | ----
`<see cref=""/>`          | `<c>`
`<paramref name=""/>`     | `<c>`
`<typeparamref name=""/>` | `<c>`
`<see langword=""/>`      | `<c>`
`<b>`                     | `<strong>`
`<i>`                     | `<em>`

The `<b>` and `<i>` preferences are deliberate, even though they're the opposite of the usual semantic-HTML advice: `<em>` isn't a recommended XML doc tag, and some tools don't process `<strong>`.

Use `<c>` sparingly; it's visually heavy. For example, use it only on the first occurrence, only when the content is highly relevant, or only when it would otherwise be ambiguous whether the text refers to code.

Avoid `<br/>`.

## Language

- Start with a capital letter.
- Start `<summary>` with a third-person verb (e.g. "Gets", "Creates", "Determines").
- Keep `<summary>` brief.
- Start `<param>`, `<typeparam>`, `<value>`, and `<returns>` with a noun.
- End with a period.
- Use consistent words and phrases.

Target                            | Pattern
--------------------------------- | -------
Constructor `<summary>`           | Initializes a new instance of the {class name} class.
Finalizer `<summary>`             | Finalizes an instance of the {class name} class.
Property `<summary>`              | Gets [or sets] [a value indicating whether]...
Boolean `<returns>` and `<value>` | true if {condition}; otherwise, false.
`<exception>`                     | {condition that completes "Thrown if..."}.

"A value indicating whether" is only for boolean properties.

A property's `<value>` can be the same as its `<summary>` without "Gets or sets"---except for boolean properties, which use the boolean pattern above.

Write `<exception>` so it completes the sentence "Thrown if..."---but omit "Thrown if" itself. For example, "<paramref name="name"/> is <see langword="null"/>." rather than "The name cannot be null." or "Thrown if the name is null."

Example:

```cs
/// <summary>
/// Represents a blog.
/// </summary>
public class Blog
{
    /// <summary>
    /// Initializes a new instance of the <see cref="Blog"/> class.
    /// </summary>
    /// <param name="name">The name of the blog.</param>
    /// <exception cref="ArgumentNullException"><paramref name="name"/> is <see langword="null"/>.</exception>
    public Blog(string name)
        => Name = name ?? throw new ArgumentNullException(nameof(name));

    /// <summary>
    /// Gets or sets the name of the blog.
    /// </summary>
    /// <value>The name of the blog.</value>
    public string Name { get; set; }

    /// <summary>
    /// Gets or sets a value indicating whether the blog is archived.
    /// </summary>
    /// <value><see langword="true"/> if the blog is archived; otherwise, <see langword="false"/>.</value>
    public bool IsArchived { get; set; }
}
```
