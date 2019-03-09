# Quickstart

Here's the simplest way to experience Vostok.Logging for the first time:

1. Install the [console log module](modules/console.md#source-and-packages).
2. Create a log instance and write your first message:

```csharp
var log = new SynchronousConsoleLog();

log.Info("Hello, {Name}!", "%username");
```

Well done! Next step is to learn about logging [syntax](concepts/syntax/), other log implementations \([console](implementations/console-log.md), [file](implementations/file-log.md), [Hercules](implementations/hercules-log.md)\) and the notion of [source context](concepts/source-context.md).

