# Quick Start

## Installing from NuGet

Dependencies: .NETStandart 2.0

```aspnet
PM> Install-Package Vostok.Logging.Abstractions -Version 0.1.1-pre000045
PM> Install-Package Vostok.Logging.Console -Version 0.1.3-pre000069
```

Browse the [Vostok.Logging tag on NuGet](https://www.nuget.org/packages?q=Vostok.Logging) to see more packages.

## SetUp

Include Vostok libraries in project:

```csharp
using Vostok.Logging.Abstractions;
using Vostok.Logging.Console;
```

Create a log using a `ConsoleLog()`.   
Create Informational log.  
Add `ConsoleLog.Flush()` for...:

```csharp
Ilog log = new ConsoleLog();
            
log.Info("Hello, {user}!", "I-430");
ConsoleLog.Flush();
```

Result:

```aspnet
2018-11-06 16:37:00,193 INFO  Hello, I-430!
```



