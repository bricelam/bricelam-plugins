---
name: csharp-native-interop
description: Conventions for writing Win32 native interop code in C# using CsWin32 (the Microsoft.Windows.CsWin32 source generator). Use whenever writing or reviewing P/Invoke calls, Win32 API usage, or native interop code in C#---even if CsWin32 isn't named explicitly, e.g. requests to call a Win32 function, work with window handles/HWNDs, or add a `NativeMethods.txt` entry.
---

# C# native interop style

Conventions for calling into Win32 via CsWin32. See the `csharp-style` skill for why CsWin32 is preferred over `DllImport`/`LibraryImport` in the first place---this skill covers how to use it once it's in the project.

## Conventions

- Add `using static Windows.Win32.PInvoke;` at the top of the file, and call generated methods and reference generated const fields directly (naked/unqualified)---don't prefix with a class name and don't wrap them in a helper method or class.
- Use the const fields CsWin32 generates as-is; don't redeclare your own copies or wrap them in an enum/class.
- Cast explicitly between `IntPtr`/`nint` and CsWin32's handle structs (`HWND`, `HANDLE`, etc.) at the boundary where a handle enters or leaves interop code, rather than avoiding the handle struct types or threading raw `IntPtr` through the rest of the code.

## Example

```csharp
using static Windows.Win32.PInvoke;
using Windows.Win32.Foundation;

HWND hwnd = (HWND)someIntPtr;
SetWindowPos(hwnd, HWND.Null, 0, 0, 0, 0, SET_WINDOW_POS_FLAGS.SWP_NOSIZE | SET_WINDOW_POS_FLAGS.SWP_NOMOVE);
```
