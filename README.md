# Quick start

We recommend [`VS Code` with `Dev Containers` extension](https://code.visualstudio.com/docs/devcontainers/containers).
The `Dev Container` extension configuration is in the `/.devcontainers/` subdirectory.
A list of additional recommended extensions is in the `/.vscode/extensions.json` file.

`debian:12` is the base for the container's image.

**NOTE:** We assume using the recommended environment.

## For those nonfamiliar with VS Code and Dev Container extension

1. Read about and install [`Docker`](https://www.docker.com/products/docker-desktop/).
2. Install `VS Code`.
3. Launch `VS Code` and install the `Dev Containers` extension.
4. Open the folder with the project using `VS Code`.
5. Reopen the project inside the container.
6. Use the `VS Code` terminal to enter all commands.

## Typical actions

1. Build the `libakmc` subproject.

```Shell
# cd /workspaces/AKMLib
cmake -S libakmc -B libakmc/out
cmake --build libakmc/out
```

2. Set up a `.NET` environment.

```Shell
# cd /workspaces/AKMLib
( cd AKMLib.NET && dotnet tool restore )
```

3. Build the `AKMLib.NET` subproject.

```Shell
# cd /workspaces/AKMLib
dotnet build AKMLib.NET
```

4. Build the documentation for `AKMLib.NET`.

```Shell
# cd /workspaces/AKMLib
( cd AKMLib.NET/Documentation && dotnet docfx -s )
# Now documentation is hosted on http://localhost:8080
# (or other port as said by VS Code)
```

5. See `dofcx` documentation for further details.

# `AKMLib`

There are two subprojects which make up the project:

```
AKMLib
|-- libakmc
`-- AKMLib.NET
```

`AKMLib.NET` depends on `libakmc`.

## libakmc

`libakmc` is a native library written in `C`. Thus, depending on the operating system, it compiles a `*.so` or `*.dll` file.

As a build system, we adopted [`CMake`](https://cmake.org/cmake/help/latest/guide/tutorial/index.html).
We recommend [`Visual Studio`](https://visualstudio.microsoft.com) for compiling Windows `*.dll`.

`AKMLib.NET` is a multiplatform `.NET` solution (`*.sln`).
There are several `C#` projects (`*.csproj`) in the `AKMLib.NET` solution:

```
AKMLib.NET
|-- AKMCommon (library)
|-- AKMInterface (library)
|-- AKMLogic (library)
|-- AKM_Tests (application)
|-- AKMWorkerService (application)
`-- AkmAutomatedTestClient (application)
```

Libraries use `netstandard2.1`, and applications use `net8.0`.

All those depend on each other as well as on external `NuGet` packages:

```
AKMInterface
`-- AKMCommon
```

```
AKMLogic
|-- AKMInterface
|-- Microsoft.Extensions.Configuration.EnvironmentVariables
|-- Microsoft.Extensions.Configuration.Json
|-- Microsoft.Extensions.Logging
|-- Microsoft.Extensions.Options.ConfigurationExtensions
`-- Newtonsoft.Json
```

```
AKM_Tests
|-- AKMLogic
|-- Microsoft.NET.Test.Sdk
|-- Moq
|-- NUnit3TestAdapter
`-- nunit
```

```
AKMWorkerService
|-- AKMLogic
|-- Microsoft.Extensions.Hosting
`-- Serilog.AspNetCore
```

```
AkmAutomatedTestClient
|-- AKMLogic
`-- Serilog.AspNetCore
```

`AKMLogic` requires `libakmc`'s `*.so` or `*.dll` file. Thanks to the rule in `/AKMLib.NET/AKMLogic/AKMLogic.csproj`, the build system looks for it in `/libakmc/out/`.
