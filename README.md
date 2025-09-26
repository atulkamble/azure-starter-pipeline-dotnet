# My Pipeline

Small .NET console application plus an Azure Pipelines definition you can use as a starting point for CI.

## Prerequisites
- .NET SDK 8.0 or newer
- Azure DevOps project with a Windows build agent (the pipeline pins `windows-2022`)

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
3. Ensure your agent has access to nuget.org. Offline agents can use an internal NuGet feed by setting up `NuGet.config` or `NuGetFallbackFolder`.

The stock YAML uses `DotNetCoreCLI` tasks to restore, build, and publish the console app. The publish stage explicitly disables web-project auto-detection and zips the published output before uploading it as a `drop` artifact. Add a `dotnet test` step once you introduce test projects.

## Housekeeping Tips
- Build outputs live under `MyApp/bin` and `MyApp/obj`; they are ignored via `.gitignore`.
- Update the pipeline image or tasks as needed if your target framework changes.
