# Log interface

Every log in Vostok.Logging implements [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs) interface. This interface exposes three methods:

| Method | Description |
| :--- | :--- |
| `Log(LogEvent)`  | Logs given [log event](log-events.md). This method is rarely invoked directly: it's preferable to use [logging extensions](syntax/logging-extensions.md). |
| `IsEnabledFor(LogLevel)` | Returns whether the current log is configured to record events of given level. This method is used in [logging extensions](syntax/logging-extensions.md) to avoid unnecessary `Log` method calls. |
| `ForContext(string)` | Returns a copy of the current log operating in given [source context](source-context.md). |

