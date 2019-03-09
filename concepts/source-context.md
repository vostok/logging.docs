# Source context

Source context is meant to denote the sources of logging events, such as classes calling the log methods. This context also encodes the hierarchy of log's ownership. It is produced with `ForContext` method and bound to returned log instance. The dominant use case for source context is to obtain class-based logs:

```csharp
class MyClass
{
    private readonly ILog log;

    public MyClass(ILog log)
    {
        this.log = log.ForContext<MyClass>();
    }
}
```



### Structure

Source context exhibits hierarchical structure: chained `ForContext` calls produce logs with multiple contexts ordered with respect to calls sequence.

```csharp
log = log
    .ForContext("foo")
    .ForContext("bar")
    .ForContext("baz"); 

// log's source context is now ["foo", "bar", "baz"]
```



### Implementation details

Handling of source context is implementation-specific. 

However, all [built-in logs](../implementations/) implement it by enriching incoming log events with a special well-known `SourceContext` property. Its value is represented by public [SourceContextValue](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/Values/SourceContextValue.cs) type that implements `IReadOnlyList<string>` and has a pretty `ToString`. This behavior can be replicated in custom log implementations by returning a [SourceContextWrapper](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/Wrappers/SourceContextWrapper.cs) from `ForContext` method.

[Serilog adapter](../integrations/serilog.md) does essentially the same.

[Log4net adapter](../integrations/log4net.md) maps source contexts to logger names.



### Rendering in text-based logs

Here's an example of how text-based logs render source context:

```csharp
var log = new SynchronousConsoleLog() as ILog;

log = log.ForContext("foo");

log.Info("Message 1");

log = log.ForContext("bar");

log.Info("Message 2");

log = log.ForContext("baz");

log.Info("Message 3");
```

Sample output from this code:

```text
2019-03-10 01:21:25,517 INFO  [foo] Message 1
2019-03-10 01:21:25,554 INFO  [foo => bar] Message 2
2019-03-10 01:21:25,555 INFO  [foo => bar => baz] Message 3
```

### Related pages

{% page-ref page="../use-cases/using-source-context.md" %}

