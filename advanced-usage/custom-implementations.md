# SMTH

### For Context

Returns a copy of the log operating in the given source context. Handling of these context strings is implementation-specific.  
Source context is not hierarchical: every `ForContext` call discards any previous context.  
If you are implementing a log and don't need this method, return `this` in the implementation.

```csharp
var log = new ConsoleLog();
var log1 = log.ForContext("context-1").ForContext("context-2");
log1.Info("0");
log1.ForContext("context-3").Debug("1");

ConsoleLog.Flush();
```

Result:

```aspnet
2019-01-18 16:23:23,517 INFO  context-2 0
2019-01-18 16:23:23,579 DEBUG context-3 1
```

