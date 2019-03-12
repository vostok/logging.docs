# Combining multiple logs

**Prerequisites**: install [abstractions module](../modules/abstractions.md).

Multiple `ILog` instances can be combined with `CompositeLog`:

```csharp
var consoleLog = new ConsoleLog();
var fileLog = new FileLog(new FileLogSettings());
var combinedLog = new CompositeLog(consoleLog, fileLog);
```

`CompositeLog` forwards incoming log events to all underlying logs.

Its `IsEnabled(LogEvent)` method returns true if any of the underlying logs is enabled for given event. 

Its `ForContext(string)` method invokes `ForContext` on all underlying logs and returns a new `CompositeLog` based on the results.

