# Assembly Metadata Resource Detector

| Status      |                                                    |
|-------------|----------------------------------------------------|
| Stability   | [Alpha](../../README.md#alpha)                     |
| Code Owners | [@austindrenski](https://github.com/austindrenski) |

[![NuGet version badge](https://img.shields.io/nuget/v/OpenTelemetry.Resources.AssemblyMetadata)](https://www.nuget.org/packages/OpenTelemetry.Resources.AssemblyMetadata)
[![NuGet download count badge](https://img.shields.io/nuget/dt/OpenTelemetry.Resources.AssemblyMetadata)](https://www.nuget.org/packages/OpenTelemetry.Resources.AssemblyMetadata)
[![codecov.io](https://codecov.io/gh/open-telemetry/opentelemetry-dotnet-contrib/branch/main/graphs/badge.svg?flag=unittests-Resources.AssemblyMetadata)](https://app.codecov.io/gh/open-telemetry/opentelemetry-dotnet-contrib?flags[0]=unittests-Resources.AssemblyMetadata)

## Getting Started

You need to install the `OpenTelemetry.Resources.AssemblyMetadata` package to be able to use the Assembly Metadata Resource Detector.

```shell
dotnet add package --prerelease OpenTelemetry.Resources.AssemblyMetadata
```

## Usage

You can add the Assembly Metadata Resource Detector to the `ResourceBuilder` as shown by the following example:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddOpenTelemetry()
    .ConfigureResource(static builder => builder.AddAssemblyMetadataDetector())
    .WithLogging(static builder => /* ... */)
    .WithMetrics(static builder => /* ... */)
    .WithTracing(static builder => /* ... */);
```

By default, the resource detector detects attributes defined on
the [entry assembly](https://learn.microsoft.com/dotnet/api/system.reflection.assembly.getentryassembly)
using [AssemblyMetadataAttribute](https://learn.microsoft.com/dotnet/api/system.reflection.assemblymetadataattribute) with keys prefixed by `otel:`.

Alternatively, you can add the resource detector with a specific [Assembly](https://learn.microsoft.com/dotnet/api/system.reflection.assembly) from
which to detect `otel:`-prefixed metadata:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddOpenTelemetry()
    .ConfigureResource(static builder => builder.AddAssemblyMetadataDetector(typeof(SomeType).Assembly))
    .WithLogging(static builder => /* ... */)
    .WithMetrics(static builder => /* ... */)
    .WithTracing(static builder => /* ... */);
```

## References

- [OpenTelemetry Project](https://opentelemetry.io/)
