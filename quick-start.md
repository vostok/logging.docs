# Quick Start

### First usage

Include Vostok libraries in project:

```csharp
using Vostok.Logging.Abstractions;
using Vostok.Logging.Console;
```

Create console log and output "Hello world!"

```csharp
var log = new ConsoleLog();
            
log.Info("Hello World!");
```

Result:

```csharp
2018-09-11 13:45:00,162 INFO Hello World!
```

