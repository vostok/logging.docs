# Enriching events

_Enriching_ is a term used to denote adding external properties to [log events](../concepts/log-events.md) after their construction. It allows to augment events with contextual information not available at immediate logging site. 

Default implementations of [source context](../concepts/source-context.md) and [operation context](../concepts/operation-context.md) involve enrichment of log events with special well-known properties.

Enrichment extensions do not overwrite properties already present in log events by default, although this can be configured.



### Enriching from constant values

**Prerequisites**: install [abstractions module](../modules/abstractions.md).

Add a property with given name and value to all log events without overwriting existing values:

```csharp
log = log.WithProperty("env", "dev");
```

Add given properties to all log events, potentially overwriting existing values:

```csharp
log = log.WithProperties(
    new Dictionary<string, object>
    {
        ["env"] = "dev",
        ["host"] = "vm-app"
    }, 
    allowOverwrite: true);
```

Add all public properties of given object to all log events:

```csharp
log = log.WithObjectProperties(new {Prop1 = 1, Prop2 = 2});
```



### Enriching from dynamic values

**Prerequisites**: install [abstractions module](../modules/abstractions.md).

Add a property with given key and value provided by given delegate to all log events:

```csharp
log = log.WithProperty("dynamicProp", () => GetPropValue());
```

Add all public properties of the object provided by given delegate to all log events:

```csharp
log = log.WithObjectProperties<CustomType>(() => GetCustomValue());
```



### Enriching from flowing context

**Prerequisites**: install [abstractions module](../modules/abstractions.md) and [context module](../modules/context.md).

Extensions listed in this section allow to enrich log events with values from `FlowingContext` exposed from [Vostok.Context](https://vostok.gitbook.io/context) library.

Add the value of the property with given name from `FlowingContext` to incoming log events with specified log name \(which may differ from property name in context\):

```csharp
log = log.WithFlowingContextProperty("contextProperty", "logProperty");
```

Add the value of the global with following type from `FlowingContext` to incoming log events with specified name:

```csharp
log = log.WithFlowingContextGlobal<CustomType>("logProperty");
```

Add all current properties from `FlowingContext` to incoming log events:

```text
log = log.WithAllFlowingContextProperties();
```

