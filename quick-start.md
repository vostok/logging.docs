# Quick Start

### First usage

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
```

Result:

```csharp
2018-09-11 13:45:00,162 INFO Hello!
```

### Advanced usage

* [UseCases](advanced-usage/usecases.md)
* [Configurations](advanced-usage/configurations.md)

