---
name: csharp-collections
description: C# collection conventions---choosing between ToList, new List, and collection-expression spread to materialize or copy a sequence, and which collection interface to use for method parameters and return types. Use whenever materializing an enumerable into a list or declaring a collection-typed parameter or return type (arrays, `List<T>`, `IEnumerable<T>`, dictionaries, etc.).
---

# C# collections

## Materialization semantics

These look interchangeable but signal different intent---pick based on what you mean, not habit.

Expression                             | Meaning
-------------------------------------- | -------
`x.ToList()`                           | Buffer/materialize a lazy `IEnumerable`; also the normal way to convert another collection type (array, `HashSet<T>`, etc.) into a `List<T>`.
`new List<T>(x)`                       | Explicitly copy/snapshot an existing collection into a new, independent `List<T>`---signals "I need my own copy of this" rather than "I need to run the query."
`[..x]` (collection-expression spread) | Don't use this to materialize or copy a list---use one of the two above instead.

## Parameter and return types

Favor the most general interface that still expresses what the implementation actually needs---this lets the caller choose between streaming and buffering instead of the signature forcing a choice.

Return types: favor `IEnumerable<T>`/`IAsyncEnumerable<T>` over `T[]`, `List<T>`, `Task<List<T>>`, etc., unless the implementation requires results to already be buffered.

Parameter types: favor `IEnumerable<T>`/`IAsyncEnumerable<T>` unless the implementation requires multiple enumerations. Use `IReadOnlyCollection<T>` when only a count is needed, or `IReadOnlyList<T>` when random access is required.

For dictionary parameters, favor `IEnumerable<KeyValuePair<TKey, TValue>>` over `IReadOnlyDictionary<TKey, TValue>`, since `IDictionary<TKey, TValue>` doesn't implement `IReadOnlyDictionary<TKey, TValue>`.
