---
name: dotnet-testing
description: Conventions for structuring and writing .NET tests---unit vs. functional test projects, naming, namespaces, directories, and Testcontainers. Use whenever creating, organizing, or writing test projects, test classes, or test methods in a .NET repo.
---

# .NET testing

## Unit tests

- Project name: `<src-project>.UnitTests`
- Class name: `<src-class>Tests`
- Class directory: match the source class
- Root namespace: same as the source project's namespace
- Use the `<InternalsVisibleTo>` MSBuild item in the source project to access non-public APIs.
- May reference the functional test project for shared test infrastructure.
- Focus more on inputs and outputs than on specific implementation.

## Functional tests

- Use Testcontainers for isolated, real dependencies.
- Don't access non-public APIs.
- Use classes and directories to group tests by area.
- Use the same class (or a base class) to share common infrastructure (e.g. setup/arrange code).
- Class names should end in Tests.

## General

- Test projects go under a `test` directory at the repo root.
- Testing infrastructure goes under a `Test/` directory in the project.
- Test method names use snake case.
- Code duplication is much more tolerable in test code. Tests should be self-contained---maintenance tasks are very different in test code compared to product code.
