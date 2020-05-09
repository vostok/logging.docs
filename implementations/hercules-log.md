# Hercules log

**Location**: [Hercules](../modules/hercules.md) module.

```csharp
var herculesLog = new HerculesLog(new HerculesLogSettings(herculesSink, logStreamName));
var dynamicallyConfiguredLog = new HerculesLog(() => ObtainSettings());
```

`HerculesLog` converts incoming [log events](../concepts/log-events.md) to [Hercules events](https://github.com/vostok/hercules/tree/master/hercules-protocol) according to [Hercules log event schema](https://github.com/vostok/hercules/blob/master/doc/event-schema/log-event-schema.md) and then sends resulting events with an instance of [IHerculesSink](https://github.com/vostok/hercules.client.abstractions/blob/master/Vostok.Hercules.Client.Abstractions/IHerculesSink.cs). Additional details on events mapping can be found in module's [description on GitHub](https://github.com/vostok/logging.hercules).



### Configuration

`HerculesLog` is configured with `HerculesLogSettings`, having 2 mandatory parameters:

| Option | Description |
| :--- | :--- |
| `HerculesSink` | An instance of sink to send events with. |
| `Stream` | Name of the Hercules stream to send events to. |

Ensure that provided sink instance is configured with an API key with sufficient permissions to write into selected stream.



### Usage tips

* Prefer to use a singleton instance of `IHerculesSink` everywhere in the application, including `HerculesLog`. Sink instances involve background tasks and are therefore quite expensive.

* Reporting of lost of log events generally depends on the nature of `IHerculesSink` implementation. Default implementation in [vostok.hercules.client](https://github.com/vostok/hercules.client) repository provides a set of counters for these purposes.

