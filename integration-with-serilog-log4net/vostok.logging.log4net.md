---
description: Represents an adapter between Vostok logging interfaces and log4net.
---

# Vostok.Logging.Log4Net

Adapter implements Vostok ILog interface using an externally provided instance of log4net ILogger.  
It does this by following these rules:

* LogLevels are directly translated to log4net Level;
* Messages are prerendered into text. \(Vostok ILog's formatting syntax differs from log4net\);
* Properties are forwarded into log4net event's LoggingEvent.Properties;
* ForContext with null argument returns a Log4netLog based on root logger from log4net's repository;
* ForContext with non-null argument returns a Log4netLog based on logger with name equal to context value, obtained with ILoggerRepository.GetLogger;

### Example

Create `ILog` with log4net. 

```csharp
private static readonly log4net.ILog log = LogManager.GetLogger(System.Reflection.MethodBase.GetCurrentMethod().DeclaringType);

static void Main(string[] args)
{
    var logRepository = LogManager.GetRepository(Assembly.GetEntryAssembly());
    XmlConfigurator.Configure(logRepository, new FileInfo("log4net.config"));
}
```

Create an adapter:

```csharp
ILog adapter = new Log4netLog(log);
```

Let's try to work with it as with Vostok's ILog:

```csharp
adapter.Warn("Let's use Vostok, please ^-^");
```



