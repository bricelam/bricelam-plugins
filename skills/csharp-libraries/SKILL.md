---
name: csharp-libraries
description: Which NuGet package or BCL API to use when several compete for the same job in C#/.NET (HTTP resilience, YAML, JSON, MVVM, ORM, logging, versioning, DB drivers, UI frameworks, etc.), which libraries to avoid, and situational libraries worth reaching for. Use whenever choosing or adding a package, or writing C# code that depends on one.
---

# C# libraries

## Preferred APIs

When a task could be solved by more than one of these, prefer the left column.

Prefer                                             | Over
-------------------------------------------------- | ----
CsWin32                                            | `DllImport`, `LibraryImport`
`HostApplicationBuilder` / `WebApplicationBuilder` | `HostBuilder`, `WebHostBuilder`
CommunityToolkit.Mvvm                              | other MVVM libraries
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
`StringLengthAttribute`                            | `MaxLengthAttribute`

## Avoid

- `DataTable`
- `System.Reflection.Emit`
- AutoMapper

## Useful libraries

Situational libraries worth reaching for when the task calls for them.

Library                                | For
-------------------------------------- | ---
Humanizer.Core                         | Pluralization and humanized string formatting
T4 + `TextTemplatingFilePreprocessor`  | Once `StringBuilder` code gets complex enough to bury the actual text content
Microsoft.Xaml.Behaviors.WinUI.Managed | XAML behaviors in WinUI apps
BenchmarkDotNet                        | Microbenchmarking
NetTopologySuite                       | Geospatial geometry operations
System.CommandLine                     | Command-line argument parsing
MimeKit                                | MIME message construction and parsing
MailKit                                | SMTP/IMAP/POP3 clients
DotNext.Threading                      | Advanced threading and async primitives
Google.Protobuf                        | Protocol Buffers serialization
CsvHelper                              | CSV reading and writing
CommunityToolkit.WinUI.*               | WinUI-specific controls, animations, behaviors, converters, and device helpers (camera, network, etc.)---check for a package before hand-rolling
