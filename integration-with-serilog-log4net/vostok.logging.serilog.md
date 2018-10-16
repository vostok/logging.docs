---
description: Represents an adapter between Vostok logging interfaces and Serilog.
---

# Vostok.Logging.Serilog

It implements Vostok ILog interface using an externally provided instance of Serilog ILogger.   
It does this by following these rules:

* Vostok LogLevel are directly translated to Serilog SerilogLevel;
* Messages are not prerendered into text as Vostok ILog's formatting syntax capabilities are a subset of those supported by Serilog;
* Message templates are parsed using ILogger.BindMessageTemplate;
* Event properties are converted using ILogger.BindProperty;
* ForContext invokes inner ILogger's ILogger.ForContext\(string,object,bool\) with name set to Constants.SourceContextPropertyNameand wraps resulting ILogger into another SerilogLog.

### Example

Допустим, используется Seriolog.

```csharp
var log = new LoggerConfiguration()
    .WriteTo.Console()
    .CreateLogger();
```

Добавим восточный фасад:

```csharp
example
```





