# Serilog integration

**Location**: [serilog](../modules/serilog.md) module.

### SerilogLog

```csharp
var serilogAdapter = new SerilogLog(serilogLogger);
```

`SerilogLog` is an adapter that wraps an arbitrary instance of Serilog's `ILogger` and implements Vostok [log interface](../concepts/log-interface.md). It enables gradual migration for Serilog users by allowing existing code to be ported to Vostok `ILog` abstraction without immediately changing and reconfiguring underlying implementation.

It preserves message templates in their original form as Serilog's templating syntax is a superset of Vostok [message templates](../concepts/syntax/message-templates.md) capabilites. Properties are also passed as-is, bound by provided Serilog logger instance.

`ForContext` method works exactly like it does in native [implementations](../implementations/): it causes returned log instances to enrich incoming log events with `SourceContext` property containing a hierarchical context value. See [source context](../concepts/source-context.md) section for more details.

### VostokSink

`VostokSink` is an implementation of Serilog's `ILogEventSink` interface based on the arbitrary Vostok `ILog` instance.

```csharp
var vostokSink = new VostokSink(vostokLog);

var serilogLogger = new LoggerConfiguration()
    .WriteTo.Sink(vostokSink, LogEventLevel.Verbose)
    .CreateLogger();
```

