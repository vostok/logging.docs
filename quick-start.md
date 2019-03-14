# Quickstart

Here's the simplest way to experience Vostok.Logging for the first time:

* Install [console](modules/console.md#source-and-packages) and [abstractions](modules/abstractions.md) modules:

```text
Install-Package Vostok.Logging.Console
Install-Package Vostok.Logging.Abstractions
```

* Create a log instance and write your first message:

```csharp
var consoleLog = new SynchronousConsoleLog();

log.Info("Hello, {Name}!", "%username%");
```

Well done! Next step is to learn about logging [syntax](concepts/syntax/), explore available [modules](modules/) and log [implementations](implementations/) and get used to the notion of [source context](concepts/source-context.md).

