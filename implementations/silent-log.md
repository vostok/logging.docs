# Silent log

**Location**: [abstractions module](../modules/abstractions.md).

```csharp
var log = new SilentLog();
```

`SilentLog` is the most trivial log implementation: it simply drops all incoming log events.

It has no configuration and is disabled for all log levels.

