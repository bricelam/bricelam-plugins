---
name: csharp-lsp
description: When to reach for the LSP tool (Roslyn language server) while working in C# code---finding a symbol's definition, references, implementations, or callers, and checking a symbol's type or signature. Use whenever answering a question about how C# code is connected (who calls this, what implements this, where is this defined, what type is this) or before changing a C# member's signature---even if Grep would get partway there.
---

# C# LSP

The LSP tool is backed by the Roslyn language server and understands C# semantically. Grep is still fine for plenty of things; the point is to not skip LSP when the question is really about symbols rather than text.

## When LSP is the better tool

Question                                           | Operation
-------------------------------------------------- | ---------
Who calls this method?                             | `incomingCalls` (after `prepareCallHierarchy`)
What does this method call?                        | `outgoingCalls` (after `prepareCallHierarchy`)
What implements this interface or abstract member? | `goToImplementation`
Where is this used?                                | `findReferences`
Where is this defined?                             | `goToDefinition`
What type is this `var` or expression?             | `hover`
What overload does this call bind to?              | `hover` or `goToDefinition`
What members does this file declare?               | `documentSymbol`
Where is a type or member with this name?          | `workspaceSymbol`

Text search tends to go wrong on these because of overloads, same-named members on unrelated types, extension methods, partial classes, inherited or explicitly implemented members, `using` aliases, and symbols from referenced assemblies or NuGet packages. A Grep that returns plausible-looking hits isn't the same as a correct answer---especially before renaming a member or changing its signature, where `findReferences` is the reliable way to find every call site.

## Getting a position

Every operation except `workspaceSymbol` needs a 1-based line and character. Use the line from Grep (`-n`) or Read, and point the character at the symbol's name---not at whitespace, a modifier, or the return type. `workspaceSymbol` needs a non-empty `query`.

## Startup

The server loads the solution on its first request, which can take a while on large repos. An empty result or timeout right at the start of a session usually means it's still loading, not that LSP doesn't work---wait briefly and retry before falling back to Grep.
