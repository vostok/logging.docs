# Operation context

Operation context represents a hierarchy of logical operations or steps in application code flow (handling a query, sending a request, performing an iteration of a periodical process).

Unlike [source context](source-context.md), operation context is bound to current [ExecutionContext](https://docs.microsoft.com/en-us/dotnet/api/system.threading.executioncontext) and can be manipulated independently of any log instances.

Operation context is maintained by defining named scopes that represent logical operations.



### Structure

Like [source context](source-context.md), operation context is also hierarchical. Nested operation scopes produce a stack-based sequence of contextual values:

```csharp
// current operation context is null
using (new OperationContextToken("op1"))
{
    // current operation context is ["op1"]
    using (new OperationContextToken("op2"))
    {
        // current operation context is ["op1", "op2"]
        using (new OperationContextToken("op3"))
        {
            // current operation context is ["op1", "op2", "op3"]
        }
        // current operation context is ["op1", "op2"]
    }
    // current operation context is ["op1"]
}
// current operation context is null
```



### Implementation details

Operation context is implemented as an extension over [log interface](log-interface.md). It can be enabled as follows:

```csharp
log = log.WithOperationContext();
```

Returned log instance will enrich incoming log events with a special well-known `OperationContext` property whose value is represented by [OperationContextValue](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/Values/OperationContextValue.cs) class.

Context scopes are started by constructing [OperationContextTokens](https://github.com/vostok/logging.context/blob/master/Vostok.Logging.Context/OperationContextToken.cs) and ended by disposing these tokens.



### Rendering in text-based logs

Here's an example of how text-based logs render operation context:

```csharp
var log = new SynchronousConsoleLog().WithOperationContext();

using (new OperationContextToken("op1"))
{
    log.Info("Message 1");

    using (new OperationContextToken("op2"))
    {
        log.Info("Message 2");

        using (new OperationContextToken("op3"))
        {
            log.Info("Message 3");
        }
    }
}
```

Sample output from this code:

```
2019-03-10 01:30:06,727 INFO  [op1] Message 1
2019-03-10 01:30:06,761 INFO  [op1] [op2] Message 2
2019-03-10 01:30:06,762 INFO  [op1] [op2] [op3] Message 3
```

### Placeholders

Operation context value can contain [placeholders](syntax/message-templates.md) filled with property values during rendering:

```
var log = new SynchronousConsoleLog().WithOperationContext();

using (new OperationContextToken("Handling-{Name}"))
{
    log.Info("Hello {Name}!", "Vostok");
}
```

Sample output from this code:

```
2022-03-02 14:41:13,784 INFO  [Handling-Vostok] Hello Vostok!
```

A property value can be passed using FlowingContext:

```
var log = new SynchronousConsoleLog().WithOperationContext().WithFlowingContextProperty("Name");

using (new OperationContextToken("Handling-{Name}"))
{
    using (FlowingContext.Properties.Use("Name", "Vostok"))
    {
        log.Info("Hello {Name}!");    
    }
}
```



### Related pages

{% content-ref url="../how-to-guides/using-operation-context.md" %}
[using-operation-context.md](../how-to-guides/using-operation-context.md)
{% endcontent-ref %}
