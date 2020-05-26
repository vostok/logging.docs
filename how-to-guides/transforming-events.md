# Transforming events

**Prerequisites**:

* Install [abstractions module](../modules/abstractions.md)
* Read about general log [configuration practices](../configuration.md)
* Read about [log interface](../concepts/log-interface.md)
* Read about [log events](../concepts/log-events.md)

Transforming extensions allows a particular `ILog` instance to modify some of incoming log events.

### Transform log level

Transform log levels of incoming log events according to provided mapping:

```csharp
log = log.WithLevelsTransformation(
    new Dictionary<LogLevel, LogLevel>
    {
        [LogLevel.Error] = LogLevel.Warn,
        [LogLevel.Fatal] = LogLevel.Warn
    });
```

Transform error log level of incoming log events to warning level:

```csharp
log = log.WithErrorsTransformedToWarns();
```

