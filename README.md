# C# Template Project

A modern C# project template with best practices and development tools configured.

## 🚀 Features

- **.NET 9.0** - Latest .NET version with cutting-edge features
- **C# Preview** - Access to the latest C# language features
- **Nullable Reference Types** - Enhanced null safety
- **Implicit Usings** - Cleaner code with reduced boilerplate
- **Embedded Debug Symbols** - Better debugging experience
- **Dev Container Support** - Consistent development environment

## 📋 Prerequisites

- [.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0) or later
- [Git](https://git-scm.com/)
- [Visual Studio Code](https://code.visualstudio.com/) (recommended)

## 📁 Project Structure

```
├── src/                    # Source code directory
├── Directory.Build.props   # MSBuild properties for all projects
├── global.json             # .NET SDK version specification
├── CODEOWNERS              # GitHub code ownership
└── README.md               # This file
```

## 🔧 Configuration

### `Directory.Build.props`

The project includes common MSBuild properties:
- **LangVersion**: `preview` - Latest C# language features
- **Nullable**: `enable` - Nullable reference types enabled
- **ImplicitUsings**: `true` - Global usings enabled
- **DebugType**: `embedded` - Embedded debug symbols

### `global.json`

Specifies .NET SDK version with `latestFeature` roll-forward policy.

## 📝 Development

### Adding New Projects

Create new projects in the `src/` directory:

```bash
dotnet new sln -n MySolution
dotnet new console -n MyProject -o src/MyProject
dotnet sln add src/MyProject/MyProject.csproj
```

### Code Style

This template follows standard C# conventions:
- Use PascalCase for public members
- Use camelCase for private fields
- Enable nullable reference types
- Use implicit usings where appropriate

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the terms specified in the [LICENSE](LICENSE) file.

## 🆘 Support

If you encounter any issues or have questions:
- Check the Issues page
- Create a new issue with detailed information
- Refer to the [.NET Documentation](https://docs.microsoft.com/dotnet/)

---

Happy coding! 🎉
