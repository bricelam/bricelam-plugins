---
name: nuget-packages
description: Convention for locating an installed NuGet package's files on disk. Use whenever inspecting a restored package's contents (e.g. reading its source, `.dll`, or `.targets` files) or otherwise needing the global packages folder path---even if the user doesn't explicitly ask about "NuGet" or "conventions."
---

# NuGet package location

Don't assume the global packages folder is `~/.nuget/packages`---that's only the default. Check the `NUGET_PACKAGES` environment variable first, since it overrides the default and is commonly set to redirect the cache elsewhere.

If it's unset, fall back to `dotnet nuget locals global-packages --list` (or `nuget locals global-packages -list`) rather than hard-coding the default path.
