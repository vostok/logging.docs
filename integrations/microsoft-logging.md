# Microsoft logging integration

**Location**: [microsoft](../modules/microsoft.md) module.

```csharp
microsoftLoggerFactory.AddVostok(vostokLog);
```

`AddVostok` extension adds a special implementation of `ILoggerProvider` from [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions) to given `ILoggerFactory`, based on provided Vostok `ILog` instance. It primarily serves to enable Vostok-based logging for AspNet.Core applications.

