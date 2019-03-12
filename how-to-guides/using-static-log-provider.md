# Using static log provider

**Prerequisites**: install [abstractions module](../modules/abstractions.md).

Abstractions module contains a static class named `LogProvider` which serves as a global shared source of `ILog` instance.

It's intended use case is logging in libraries: library authors may not want to force their users to provide an `ILog` instance each time they're using library classes. Instead, these classes could just obtain a log from `LogProvider`:

```csharp
LogProvider.Get().Info("library code message");
```

User application or underlying host may choose to explicitly configure `LogProvider` in order to enable this logging:

```csharp
LogProvider.Configure(new ConsoleLog());
```

By default, `Get` method returns an instance of [silent log](../implementations/silent-log.md).

