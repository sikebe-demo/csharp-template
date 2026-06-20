# C# Template Project

Modern C# project template with .NET 9.0, best practices, and development tools configured.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Prerequisites and Environment Setup
- Install .NET 9.0 SDK (required version: 9.0.304):
  - `curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin --version 9.0.304` -- takes 30-60 seconds to complete. NEVER CANCEL. Set timeout to 90+ seconds.
  - `export PATH="$HOME/.dotnet:$PATH"` (add to your session)
  - Verify: `dotnet --version` should return `9.0.304`

### Project Creation and Build Process
- Create a new console application:
  - `dotnet new console -n MyProject -o src/MyProject`
  - `dotnet new sln -n MySolution` (if no solution exists)
  - `dotnet sln add src/MyProject/MyProject.csproj`
- Build the project:
  - `dotnet build` -- takes ~5 seconds. Set timeout to 30+ seconds for safety.
  - `dotnet build --configuration Release` (optimized release build)
  - `dotnet build --verbosity normal` (for detailed output including warnings)
  - `dotnet build --no-restore` (skip package restore if already done)
- Run the application:
  - `dotnet run --project src/MyProject`
  - `dotnet run --project src/MyProject --configuration Release`
- Clean build artifacts:
  - `dotnet clean`
  - `dotnet clean --configuration Release`

### Testing
- Create test project:
  - `dotnet new xunit -n MyProject.Tests -o src/MyProject.Tests`
  - `dotnet sln add src/MyProject.Tests/MyProject.Tests.csproj`
  - Add project reference: `dotnet add src/MyProject.Tests reference src/MyProject/MyProject.csproj`
- Run tests:
  - `dotnet test` -- takes ~5 seconds including build. Set timeout to 30+ seconds.
  - `dotnet test --verbosity normal` (for detailed test output)
  - `dotnet test --logger trx` (for test result files)

### Code Quality and Formatting
- Format code (ALWAYS run before committing):
  - `dotnet format` -- formats according to .editorconfig rules
  - `dotnet format --verify-no-changes` (check if formatting is needed)
  - `dotnet format --verbosity diagnostic` (detailed formatting output)

## Validation

### Manual Validation Steps
- ALWAYS run through this validation after making changes to ensure the template works correctly:
  1. Create a sample console application: `dotnet new console -n TestApp -o src/TestApp`
  2. Create solution if needed: `dotnet new sln -n TestSolution`
  3. Add project to solution: `dotnet sln add src/TestApp/TestApp.csproj`
  4. Build the project: `dotnet build` (should complete in ~5 seconds)
  5. Run the application: `dotnet run --project src/TestApp` (should output "Hello, World!")
  6. Create and run tests: `dotnet new xunit -n TestApp.Tests -o src/TestApp.Tests && dotnet sln add src/TestApp.Tests/TestApp.Tests.csproj && dotnet test`
  7. Format and verify formatting: `dotnet format && dotnet format --verify-no-changes`
  8. Clean up: `rm -rf src/TestApp src/TestApp.Tests TestSolution.sln`

### Expected Build Behavior
- Initial builds may take longer due to package restoration
- Subsequent builds are very fast (~5 seconds)
- No warnings should appear with default template settings
- All projects inherit settings from Directory.Build.props

## Configuration and Important Files

### Key Configuration Files
- `global.json` - Specifies .NET SDK version (9.0.304) with latestFeature rollForward
- `Directory.Build.props` - MSBuild properties applied to all projects:
  - LangVersion: preview (latest C# features)
  - Nullable: enable (nullable reference types)
  - ImplicitUsings: true (global usings enabled)
  - DebugType: embedded (embedded debug symbols)
  - NoWarn: CA2254 (suppresses specific analyzer warning)
- `.editorconfig` - Code style and formatting rules
- `.devcontainer/devcontainer.json` - Dev container configuration with pre-installed extensions

### Project Structure
```
├── .devcontainer/          # Dev container configuration
├── .github/                # GitHub configuration and workflows
├── src/                    # Source code directory (initially empty with .gitkeep)
├── Directory.Build.props   # MSBuild properties for all projects
├── global.json            # .NET SDK version specification
├── .editorconfig          # Code style and formatting rules
├── .gitignore             # Git ignore patterns
├── CODEOWNERS             # Code ownership configuration
└── README.md              # Project documentation
```

## Common Tasks

### Creating Different Project Types
- Console application: `dotnet new console -n ProjectName -o src/ProjectName`
- Class library: `dotnet new classlib -n ProjectName -o src/ProjectName`
- Web API: `dotnet new webapi -n ProjectName -o src/ProjectName`
- MVC Web App: `dotnet new mvc -n ProjectName -o src/ProjectName`
- Blazor Server: `dotnet new blazorserver -n ProjectName -o src/ProjectName`
- Worker Service: `dotnet new worker -n ProjectName -o src/ProjectName`
- xUnit test project: `dotnet new xunit -n ProjectName.Tests -o src/ProjectName.Tests`
- NUnit test project: `dotnet new nunit -n ProjectName.Tests -o src/ProjectName.Tests`
- MSTest test project: `dotnet new mstest -n ProjectName.Tests -o src/ProjectName.Tests`

### Common NuGet Packages
- Logging: `dotnet add package Microsoft.Extensions.Logging`
- HTTP Client: `dotnet add package Microsoft.Extensions.Http`
- Configuration: `dotnet add package Microsoft.Extensions.Configuration`
- Dependency Injection: `dotnet add package Microsoft.Extensions.DependencyInjection`
- Entity Framework Core: `dotnet add package Microsoft.EntityFrameworkCore`
- AutoMapper: `dotnet add package AutoMapper`
- FluentValidation: `dotnet add package FluentValidation`
- Newtonsoft.Json: `dotnet add package Newtonsoft.Json`

### Working with Solutions
- Create solution: `dotnet new sln -n SolutionName`
- Add project to solution: `dotnet sln add src/ProjectName/ProjectName.csproj`
- List projects in solution: `dotnet sln list`
- Remove project from solution: `dotnet sln remove src/ProjectName/ProjectName.csproj`
- Build entire solution: `dotnet build` (from solution directory)

### Working with Project References
- Add project reference: `dotnet add src/ProjectA reference src/ProjectB/ProjectB.csproj`
- Remove project reference: `dotnet remove src/ProjectA reference src/ProjectB/ProjectB.csproj`
- List project references: `dotnet list src/ProjectA reference`

### Package Management
- Add package reference: `dotnet add src/ProjectName package PackageName`
- Add specific version: `dotnet add src/ProjectName package PackageName --version 1.2.3`
- Remove package reference: `dotnet remove src/ProjectName package PackageName`
- List package references: `dotnet list src/ProjectName package`
- List outdated packages: `dotnet list src/ProjectName package --outdated`
- Restore packages: `dotnet restore`

### Publishing and Deployment
- Publish for current platform: `dotnet publish src/ProjectName --configuration Release`
- Publish self-contained: `dotnet publish src/ProjectName --configuration Release --self-contained`
- Publish for specific runtime: `dotnet publish src/ProjectName --configuration Release --runtime win-x64`
- Publish single file: `dotnet publish src/ProjectName --configuration Release --runtime linux-x64 --self-contained --publish-single-file`

### Development Workflow
1. Create your project structure using the commands above
2. Build frequently: `dotnet build`
3. Run tests regularly: `dotnet test`
4. For web applications: `dotnet run` starts the development server (typically on localhost:5000-5001 for HTTPS, or as shown in console output)
5. Format code before committing: `dotnet format`
6. Verify no formatting issues: `dotnet format --verify-no-changes`

### Web Application Development
- Run web application: `dotnet run` (check console output for the listening URL)
- Run with specific environment: `dotnet run --environment Production`
- Run with hot reload: `dotnet watch run` (automatically restarts on file changes)
- HTTPS development certificate: `dotnet dev-certs https --trust` (run once per machine)

### Performance and Diagnostics
- Build with optimizations: `dotnet build --configuration Release`
- Time build: `time dotnet build` (to measure build performance)
- Verbose output: `dotnet build --verbosity diagnostic`
- No-op build check: `dotnet build --no-restore --no-dependencies` (to check if rebuild is needed)

## Troubleshooting

### Common Issues
- **SDK version mismatch**: Ensure .NET 9.0.304 is installed and PATH is updated
- **Build failures**: Run `dotnet clean` then `dotnet restore` followed by `dotnet build`
- **Formatting errors**: Run `dotnet format` to auto-fix most issues
- **Missing packages**: Run `dotnet restore` to restore NuGet packages
- **Dev container issues**: Rebuild container if extensions are not working

### Verification Commands
- Check .NET version: `dotnet --version`
- List installed SDKs: `dotnet --list-sdks`
- Check solution status: `dotnet sln list`
- Verify project builds: `dotnet build --verbosity normal`

## Additional Notes
- The template is configured for modern C# development with nullable reference types enabled
- All projects automatically inherit common MSBuild properties from Directory.Build.props
- The dev container includes GitHub Copilot and C# development extensions
- Code style enforcement is configured via .editorconfig with specific rules for C# files
- Build times are very fast (~5 seconds) due to the minimal template structure