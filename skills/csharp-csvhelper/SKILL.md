---
name: csharp-csvhelper
description: Conventions for using CsvHelper in C#. Use whenever writing or reviewing code that reads or writes CSV with CsvHelper, or whenever using CsvHelper's `FormatAttribute`, `IgnoreAttribute`, `NameAttribute`, or `TypeConverterAttribute`---even if CsvHelper isn't named explicitly.
---

# C# CsvHelper style

Conventions for using CsvHelper. See the `csharp-style` skill for why CsvHelper is preferred for CSV reading/writing in the first place---this skill covers how to use it once it's in the project.

## Type aliases

Several CsvHelper attribute types are named too generically (`FormatAttribute`, `IgnoreAttribute`, `NameAttribute`, `TypeConverterAttribute`) and collide with similarly-named types elsewhere (e.g. `System.ComponentModel.TypeConverterAttribute`). Always rename them for clarity with a `using` alias directive:

```cs
using CsvFormatAttribute = CsvHelper.Configuration.Attributes.FormatAttribute;
using CsvIgnoreAttribute = CsvHelper.Configuration.Attributes.IgnoreAttribute;
using CsvNameAttribute = CsvHelper.Configuration.Attributes.NameAttribute;
using CsvTypeConverter = CsvHelper.Configuration.Attributes.TypeConverterAttribute;
```
