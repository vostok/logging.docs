---
description: Represents an adapter between Vostok logging interfaces and log4net.
---

# Vostok.Logging.Log4Net

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









