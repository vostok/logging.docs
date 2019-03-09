# Configuration

This page describes approaches to configuration employed in Vostok.Logging.

### Composing loggers hierarchy

There's no such thing as a log factory or log provider: there are just [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs) instances, and the only way to get one initially is to instantiate one of the available [implementations](implementations/) in code. Everything else is achieved with decorator-based extensions and interface methods:

* [Combining](use-cases/combining-multiple-logs.md) multiple logs into one.
* [Filtering](use-cases/filtering-events-by-level.md) incoming events.
* [Enriching](use-cases/enriching-events-with-custom-properties.md) incoming events with properties.
* Obtaining log instances tied to specific [source context](concepts/source-context.md).

This approach may look unfamiliar to prior [log4net](https://logging.apache.org/log4net/) users experienced with [XML configuration files](https://logging.apache.org/log4net/release/manual/configuration.html). Indeed, it lacks additional flexibility offered by file-based configs but enables much easier setup for new applications.

### Injecting loggers into code

It's preferable to inject log instances explicitly through constructors, either using a DI container or simply passing them manually. [Static log provider](use-cases/using-static-log-provider.md) is supported but not recommended.

### Configuring individual loggers

Individual log instances \(such as [console log](implementations/console-log.md) or [file log](implementations/file-log.md)\) are typically configured in code by passing a settings object. However, some implementations \(namely [file log](implementations/file-log.md)\) also accept an arbitrary settings provider delegate that can be used to configure from external sources using [Vostok.Configuration](https://vostok.gitbook.io/configuration/) library.

