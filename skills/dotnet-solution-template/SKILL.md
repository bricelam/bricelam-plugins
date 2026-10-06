---
name: dotnet-solution-template
description: Repo-root config files, license, and CI for a brand-new .NET repo. Use whenever starting a new .NET repo from scratch, not when adding a project to an existing one.
---

# .NET solution template

Bundled repo-root files (`template/` next to this SKILL.md) to drop into a brand-new .NET repo before creating any projects. Copy them as-is---no placeholders to fill in.

## Steps

1. `git init` the new repo if it isn't one already; the version files below need a git repo to work correctly.
2. Copy everything from `template/` into the repo root, preserving paths (`.github/workflows/cicd.yml`, `.github/dependabot.yml` included).
3. Fetch the current `.gitignore` from `https://raw.githubusercontent.com/github/gitignore/main/VisualStudio.gitignore` and save it as `.gitignore` in the repo root---don't use a locally cached/older copy.
4. Create `LICENSE.md` based on what the repo is for:

   Repo is...         | License                              | Source
   ------------------ | ------------------------------------ | ------
   A reusable library | Ms-PL (Microsoft Public License)     | Copy `licenses/Ms-PL.md`
   An app             | Ms-RL (Microsoft Reciprocal License) | Copy `licenses/Ms-RL.md`
   Just example code  | The Unlicense                        | Fetch `https://unlicense.org/UNLICENSE`

   If it's unclear which the repo is, ask before picking one.
5. Commit before building---`Nerdbank.GitVersioning` (wired in via `Directory.Packages.props`) computes the version from git history and needs at least one commit.
6. Create the solution and projects with the `dotnet` CLI (`dotnet new sln`, `dotnet new classlib`/`console`/etc., `dotnet sln add`)---`cicd.yml` builds/tests the solution, so projects added to it don't need any CI changes.
7. Because `Directory.Packages.props` turns on central package management, add package versions there (`<PackageVersion Include="..." Version="..." />`), not in individual `.csproj` files---package references in project files omit the `Version` attribute.
8. `global.json` pins the test runner to `Microsoft.Testing.Platform`---use xunit.v3 (which runs on MTP) for test projects rather than the legacy VSTest-based setup. See the `dotnet-testing` skill for test project conventions.

## What's deliberately not included

No `README`---add one per-repo since it varies by project.
