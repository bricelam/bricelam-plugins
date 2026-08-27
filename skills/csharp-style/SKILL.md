---
name: csharp-style
description: C#/.NET conventions---which library or API to reach for when several compete for the same job, and the exact semantics of ToList, new List, and collection-expression spread. Use this whenever writing, reviewing, or suggesting C#/.NET code, whenever choosing a NuGet package or BCL API for a task (HTTP resilience, YAML, MVVM, testing, ORM, versioning, DB drivers, etc.), and whenever materializing an enumerable sequence into a list---even if the user doesn't explicitly ask for "style" or "conventions."
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

For raw Win32/CsWin32 interop conventions (not just "prefer CsWin32 over DllImport"), see the `csharp-native-interop` skill.

### Avoid

- `DataTable`
- `System.Reflection.Emit`

## Collection materialization semantics

These three look interchangeable but signal different intent---pick based on what you mean, not habit.

Expression                             | Meaning
-------------------------------------- | -------
`x.ToList()`                           | Buffer/materialize a lazy `IEnumerable`; also the normal way to convert another collection type (array, `HashSet<T>`, etc.) into a `List<T>`.
`new List<T>(x)`                       | Explicitly copy/snapshot an existing collection into a new, independent `List<T>`---signals "I need my own copy of this" rather than "I need to run the query."
`[..x]` (collection-expression spread) | Syntax abuse. Never use this to materialize or copy a list---use one of the two above instead.
