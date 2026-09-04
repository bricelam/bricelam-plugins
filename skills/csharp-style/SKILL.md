---
name: csharp-style
description: C#/.NET conventions---which library or API to reach for when several compete for the same job, the exact semantics of ToList, new List, and collection-expression spread, how to write a LINQ query expression that ends in a method call, and which collection interface to use for method parameters and return types. Use this whenever writing, reviewing, or suggesting C#/.NET code, whenever choosing a NuGet package or BCL API for a task (HTTP resilience, YAML, MVVM, testing, ORM, versioning, DB drivers, etc.), whenever materializing an enumerable sequence into a list, whenever a LINQ query expression (`from`...`select`) needs a trailing call like `Count()` or `ToList()`, and whenever declaring a method's parameter or return type that is a collection (arrays, `List<T>`, `IEnumerable<T>`, dictionaries, etc.)---even if the user doesn't explicitly ask for "style" or "conventions."
---

# C# style

Conventions for C#/.NET code. Apply these by default; only deviate if the user says otherwise or the project already has an established, different convention.

## Preferred APIs

When a task could be solved by more than one of these, prefer the left column.

Prefer                                             | Over
-------------------------------------------------- | ----
CsWin32                                            | `DllImport`, `LibraryImport`
`HostApplicationBuilder` / `WebApplicationBuilder` | `HostBuilder`, `WebHostBuilder`
CommunityToolkit.Mvvm                              | other MVVM libraries
xunit.v3                                           | NUnit, MSTest
Win2D                                              | other DirectX interop
Nerdbank.GitVersioning                             | any other versioning strategy
Dapper                                             | `DbCommand.ExecuteReader` (raw ADO.NET)
YamlDotNet                                         | other YAML libraries
`System.Text.Json`                                 | Newtonsoft.Json / JSON.NET
`Microsoft.Data.SqlClient`                         | `System.Data.SqlClient`
EF Core                                            | NHibernate, EF6
`Azure.Monitor.OpenTelemetry.Exporter`             | other Application Insights APIs
`Microsoft.Extensions.Http.Resilience`             | direct Polly APIs
Pomelo.EntityFrameworkCore.MySql                   | MySql.EntityFrameworkCore
MySqlConnector                                     | MySql.Data
`Microsoft.Data.Sqlite`                            | `System.Data.SQLite`
`DbDataReader.GetColumnSchema`                     | `DbDataReader.GetSchemaTable`
`XDocument`                                        | `XmlDocument`
WinUI / Uno                                        | MAUI/Xamarin, Avalonia, WPF, WinForms
WinUIEx                                            | hand-rolled Win32 interop for window chrome/positioning
`Microsoft.Extensions.Logging`                     | Serilog, NLog, log4net
`System.IO.Compression` & `System.Formats.Tar`     | SharpZipLib

For raw Win32/CsWin32 interop conventions (not just "prefer CsWin32 over DllImport"), see the `csharp-native-interop` skill.

### Avoid

- `DataTable`
- `System.Reflection.Emit`
- Moq
- AutoMapper
- FluentAssertions

## Useful libraries

Situational libraries worth reaching for when the task calls for them, rather than blanket preferences like the table above.

Library                                                                   | For
------------------------------------------------------------------------- | ---
Humanizer.Core                                                            | Pluralization and humanized string formatting
T4 + `TextTemplatingFilePreprocessor`                                     | Reaching for once `StringBuilder` code gets complex enough to bury the actual text content
Microsoft.Xaml.Behaviors.WinUI.Managed + CommunityToolkit.WinUI.Behaviors | XAML behaviors in WinUI apps
BenchmarkDotNet                                                           | Microbenchmarking
NetTopologySuite                                                          | Geospatial geometry operations
System.CommandLine                                                        | Command-line argument parsing
MimeKit                                                                   | MIME message construction and parsing
MailKit                                                                   | SMTP/IMAP/POP3 clients
DotNext.Threading                                                         | Advanced threading and async primitives
Google.Protobuf                                                           | Protocol Buffers serialization
CsvHelper                                                                 | CSV reading and writing

## Query syntax with a trailing method call

A query expression (`from`...`select`) has no method syntax of its own for calls like `Count` or `ToList`---don't bolt one on by parenthesizing the whole expression. Instead, pass the query expression as an argument to the equivalent `Enumerable`/`Queryable` static method.

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

## Collection materialization semantics

These three look interchangeable but signal different intent---pick based on what you mean, not habit.

Expression                             | Meaning
-------------------------------------- | -------
`x.ToList()`                           | Buffer/materialize a lazy `IEnumerable`; also the normal way to convert another collection type (array, `HashSet<T>`, etc.) into a `List<T>`.
`new List<T>(x)`                       | Explicitly copy/snapshot an existing collection into a new, independent `List<T>`---signals "I need my own copy of this" rather than "I need to run the query."
`[..x]` (collection-expression spread) | Syntax abuse. Never use this to materialize or copy a list---use one of the two above instead.

## Collection interface guidance

Favor the least-committal interface that still expresses what the implementation actually needs---this lets the caller choose between streaming and buffering instead of the signature forcing a choice.

Return types: favor `IEnumerable<T>`/`IAsyncEnumerable<T>` over `T[]`, `List<T>`, `Task<List<T>>`, etc., unless the implementation requires results to already be buffered.

Parameter types: favor `IEnumerable<T>`/`IAsyncEnumerable<T>` unless the implementation requires multiple enumerations. Use `IReadOnlyCollection<T>` when only a count is needed, or `IReadOnlyList<T>` when random access is required.

For dictionary parameters, favor `IEnumerable<KeyValuePair<TKey, TValue>>` over `IReadOnlyDictionary<TKey, TValue>`, since `IDictionary<TKey, TValue>` doesn't implement `IReadOnlyDictionary<TKey, TValue>`.
