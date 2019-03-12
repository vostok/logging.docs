# Log4net integration

**Location**: [log4net](../modules/log4net.md) module.

```csharp
var log4netAdapter = new Log4netLog(log4netLogger);
```

`Log4netLog` is an adapter that wraps an arbitrary instance of Log4net's `ILogger` and implements Vostok [log interface](../concepts/log-interface.md). It enables gradual migration for Log4net users by allowing existing code to be ported to Vostok `ILog` abstraction without immediately changing and reconfiguring underlying implementation.

`Log4netLog` prerenders messages into text as Log4net library does not support all the syntax capabilities of Vostok [message templates](../concepts/syntax/message-templates.md). Properties are passed as-is.

`ForContext` method implementation differs from common conventions described in [source context](../concepts/source-context.md) section. It translates source context values into logger names by using a configurable `LoggerNameFactory` delegate. Having determined the new logger name, it returns a copy of the log with underyling `ILogger` obtained from current `ILogger`'s repository by this name.

Default behaviour of `LoggerNameFactory` is to merge context values using dot as separator:

```text
["foo", "bar", "baz"] context --> "foo.bar.baz" logger name
```

Here's how to configure it to use only the last value from source context:

```csharp
log.LoggerNameFactory = context => context.Last();
```

