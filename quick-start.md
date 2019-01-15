# Quick Start

## Installing from NuGet

Dependencies: .NETStandard 2.0

```aspnet
PM> Install-Package Vostok.Logging.Console
```

Browse the [Vostok.Logging tag on NuGet](https://www.nuget.org/packages?q=Vostok.Logging) to see more packages.

## SetUp

Include Vostok libraries in project:

```csharp
using Vostok.Logging.Abstractions;
using Vostok.Logging.Console;
```

Use the `ConsoleLog()` and log an informational message.  
Since the log is asynchronous, add `Flush()` to record the message before the program ends:

```csharp
Ilog log = new ConsoleLog();  
log.Info("Hello, {user}!", "I-430");

ConsoleLog.Flush();
```

Result:

```aspnet
2018-11-06 16:37:00,193 INFO  Hello, I-430!
```

##   

Read more about syntax features, out-of-the-box implementations and advanced usage:

{% page-ref page="syntax.md" %}

{% page-ref page="implementations/" %}

{% page-ref page="advanced-usage.md" %}



