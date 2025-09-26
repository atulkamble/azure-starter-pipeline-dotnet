# My Pipeline

Small .NET console application plus an Azure Pipelines definition you can use as a starting point for CI.

## Prerequisites
- .NET SDK 9.0 (ships with backward compatible tooling for .NET 7)
- Azure DevOps project with a Windows build agent (the provided pipeline uses `windows-latest`)

## Running Locally
Restore, build, and run the app from the repo root:

```bash
dotnet restore MyApp/MyApp.sln
dotnet build MyApp/MyApp.sln
dotnet run --project MyApp/MyApp.csproj
```

The console prints a greeting and the current timestamp.

## Continuous Integration
1. Import the repo into Azure DevOps.
2. Create a pipeline and point it at `azure-pipelines.yml`.
3. Ensure your agent has access to nuget.org. Offline agents can use an internal NuGet feed by setting up `NuGet.config`.

The stock YAML includes NuGet restore, Visual Studio build, and VSTest steps. Adjust or replace these tasks if you convert the app to use cross-platform `dotnet` CLI builds or add real test projects.

## Housekeeping Tips
- Add the standard `bin/` and `obj/` directories to `.gitignore` so compiled artifacts stay out of source control.
- Consider upgrading `MyApp/MyApp.csproj` to a supported target framework (for example, `net8.0`) to avoid .NET end-of-support warnings.
