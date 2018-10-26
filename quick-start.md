# Quick Start

## Installing from NuGet

Dependencies: .NETStandart 2.0

```aspnet
PM> Install-Package Vostok.Logging.Abstractions -Version 0.1.1-pre000044
PM> Install-Package Vostok.Logging.Console -Version 0.1.1-pre000051
```

Browse the [Vostok.Logging tag on NuGet](https://www.nuget.org/packages?q=Vostok.Logging) to see more packages.

## First usage

Let's try Vostok and write a simple program.

Include Vostok libraries in project:

```csharp
using Vostok.Logging.Abstractions;
using Vostok.Logging.Console;
```

Create a log using a `ConsoleLog()` :

```csharp
Ilog log = new ConsoleLog();
            
log.Info("Hello!");
ConsoleLog.Flush();
```

Result:

```csharp
2018-09-11 13:45:00,162 INFO Hello!
```

## Advanced usage

* [UseCases]()
* [Configurations]()

