# External configuration rules

**Prerequisites**:

* Install [configuration module](../modules/configuration.md)
* Read about [log events](../concepts/log-events.md)
* Read about [source context](../concepts/source-context.md)
* Read about [filtering](filtering-events-by-level.md)
* Read about [enrichment](enriching-events-with-custom-properties.md)

[ConfigurableLog](https://github.com/vostok/logging.configuration/blob/master/Vostok.Logging.Configuration/ConfigurableLog.cs) is essentially a [CompositeLog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/CompositeLog.cs) with named components and [rules](https://github.com/vostok/logging.configuration/blob/master/Vostok.Logging.Configuration/LogConfigurationRule.cs) for filtering and enrichment. Rules can be supplied from any external source and support reconfiguration without application restart.

### Log configuration rules

Every rule contains some of the following:

| **Property** | Type | **Default value** | **Description** |
| :--- | :--- | :--- | :--- |
| **Enabled** | `bool` | `true` | Enables/disables the logging in scope of the rule entirely. |
| **Log** | `string` | `null` | Limits the scope of the rule to the log with given name. If not specified, the rule applies to all logs. |
| **Source** | `string` | `null` | Limits the scope of the rule to events with source context having given prefix. |
| **MinimumLevel** | `LogLevel?` | `null` | Sets the minimum log level for the events in scope of the rule. |
| **Properties** | `Dictionary` | `null` | Adds given set of properties to every event in scope of the rule. |

### Create a ConfigurableLog

```csharp
var rules = new[]
{
    new LogConfigurationRule { Log = "c1", Source = "noisy", MinimumLevel = LogLevel.Warn},
    new LogConfigurationRule { Log = "c2", Enabled = false },
    new LogConfigurationRule { Log = "c3", Properties = new Dictionary<string, string> { ["key"] = "value" } }
};

var log = new ConfigurableLogBuilder()
    .AddLog("c1", new SynchronousConsoleLog())
    .AddLog("c2", new SynchronousConsoleLog())
    .AddLog("c3", new SynchronousConsoleLog())
    .SetRules(rules)
    .Build();
```

Rules can also be supplied with an `IObservable<LogConfigurationRule[]>`. Here's an equivalent of the configuration above using [Vostok.Configuration](https://github.com/vostok/configuration) library and storing rules in JSON file:

```csharp
var source = new JsonFileSource("log-rules.json");
var rulesObservable = ConfigurationProvider.Default.Observe<LogConfigurationRule[]>(source);

var log = new ConfigurableLogBuilder()
    .AddLog("c1", new SynchronousConsoleLog())
    .AddLog("c2", new SynchronousConsoleLog())
    .AddLog("c3", new SynchronousConsoleLog())
    .SetRules(rulesObservable)
    .Build();
```

```csharp
[
    { "Log": "c1", "Source": "noisy", "MinimumLevel": "Warn" },
    { "Log": "c2", "Enabled": "false" },
    { "Log": "c3", "Properties": { "key": "value" } }
]
```

