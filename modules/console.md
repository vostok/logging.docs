# Console

### Description

This library contains an [implementation](../implementations/console-log.md) of ILog that writes events to console output. Implementation comes in two flavors: [ConsoleLog](https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLog.cs) \(default, async\) and [SynchronousConsoleLog ](https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/SynchronousConsoleLog.cs)\(well-suited for tests and debugging\).

### Source and packages

**GitHub repository:** [vostok/logging.console](https://github.com/vostok/logging.console)

**NuGet package**: [Vostok.Logging.Console](https://www.nuget.org/packages/Vostok.Logging.Console)

```text
Install-Package Vostok.Logging.Console
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```text
cm ref add vostok.logging.console <path-to-project>
```

### Related pages

{% page-ref page="../implementations/console-log.md" %}

