# Interaction with other Vostok libraries

The main value of Vostok.Logging – integration with other Vostok's libraries. 

### Logging + [Context](https://vostok.gitbook.io/context/)

[Logging.Context](https://github.com/vostok/logging.context) enables us to say: "Let's automatic add properties from context to that log".  
If you use `ContextualLogPrefix`, you can do so:

```csharp
var log = new ConsoleLog().WithContextualPrefix();

using (new ContextualLogPrefix("op-1"))
{
    log.Info("Message 1!");
    
    using (new ContextualLogPrefix("op-2"))
    {
        log.Info("Message 2!");
    }               
    
    log.Info("Message 3!");
}
ConsoleLog.Flush();
```

Result:

```aspnet
2018-12-11 16:06:37,970 INFO  [op-1] Message 1!
2018-12-11 16:06:38,047 INFO  [op-1] [op-2] Message 2!
2018-12-11 16:06:38,047 INFO  [op-1] Message 3!
```

### Logging + Hercules

[Logging.Hercules](https://github.com/vostok/logging.hercules) – library is for a log which output events to Hercules.

LogEvent instances are mapped into Hercules events by this rules:

* `Timestamp` \(mandatory\) corresponds to:
  * Hercules event build-timestamp - a `UtcDateTime` of `Timestamp`.
  * `UtcOffset` tag - a `long` tag with offset from UTC expressed in 100-ns ticks. 
* `MessageTemplate` ---&gt; `MessageTemplate` tag of `string` type. 
* `RenderedMessage` ---&gt; `MessageTemplate` rendered to log string with templates replaced to corresponding values from `Properties`. 
* `Properties` dictionary corresponds to a container with the same name. This container contains a tag for each pair. Keys are translated as-is, and the values are handled according to following conventions:
  * If the value is a primitive scalar or a vector of primitive scalars natively supported by Hercules \(such as `int`, `long`, `guid`, `string`, etc\), it's mapped as-is.
  * Otherwise the value gets converted to `string`: either stringified directly \(if it properly overrides `ToString()`\) or serialized to JSON. No further container-like structure is allowed, all values end up being 'flat'. 
* `Exception` object corresponds to a container with the same name and following tags:
  * Exception runtime type \(e.g. `System.NullReferenceException`\) ---&gt; `Type` tag of type `string`.
  * Exception message ---&gt; `Message` tag of type `string`.
  * Nested exceptions \(e.g. `InnerException` and `InnerExceptions` for `AggregateException`\) ---&gt; `InnerExceptions` tag of type `Vector` which contains other exceptions in the same format.
  * Stacktrace of exception ---&gt; `StackTrace` tag of type `Vector` of `StackFrame`. `StackFrame` is `Container` of the following tags which describe a point of code which executed when exception occured:
    * `Function` - a name of function \(method\).
    * `Type` - a type when `Function` is declared.
    * `File` - file name.
    * `Line` - line number.
    * `Column` - column number.

### Logging + Tracing

... – library is for adding TraceId to logs.

