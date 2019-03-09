# Quickstart

Here's the simplest way to experience Vostok.Logging for the first time:

1. Install [console](modules/console.md#source-and-packages) and [abstractions](modules/abstractions.md) modules.
2. Create a log instance and write your first message:

```csharp
var consoleLog = new SynchronousConsoleLog();

log.Info("Hello, {Name}!", "%username");
```

Well done! Next step is to learn about logging [syntax](concepts/syntax/), explore all [modules](modules/) and log implementations \([console](implementations/console-log.md), [file](implementations/file-log.md), [Hercules](implementations/hercules-log.md)\) and get used to the notion of [source context](concepts/source-context.md).

