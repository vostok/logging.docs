# Using operation context

This page lists preparation steps required to begin using [operation context](../concepts/operation-context.md) in application logs.

**Prerequisites**: install [context module](../modules/context.md), read [operation context](../concepts/operation-context.md) section.

**Step 1**: enable operation context on a log instance using `WithOperationContext()` extension:

```csharp
log = log.WithOperationContext();
```

**Step 2**: define context scopes by constructing and disposing `OperationContextToken`s:

```csharp
using (new OperationContextToken("op1")) 
{
    // log something
    using (new OperationContextToken("op2")
    {
        // log something
    }
}
```

There's also an `ILog` extension named `ForOperationContext` which is just a convenient shortcut for creating `OperationContextToken`s and does not really depend on an `ILog` instance:

```csharp
using (log.ForOperationContext("op")) { }
```

