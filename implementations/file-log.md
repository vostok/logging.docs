# File log

**Location**: [file module](../modules/file.md).

```csharp
var fileLog = new FileLog(new FileLogSettings());
var dynamicallyConfiguredLog = new FileLog(() => ObtainSettings());
```



### Features

* Customizable [output templates](../concepts/formatting/output-templates.md).
* Customizable rolling strategies:
  * By size (roll over to a new file when current one reaches given size)
  * By time (roll over to a new file every second/minute/hour/day)
  * Hybrid (both by size and time)
  * Automatic cleanup of stale files
* Multiplexing: multiple `FileLog` instances inside a single process may write to the same file without performance penalties.
* `Log` method is nonblocking: log events are placed into an internal queue, buffered and efficiently written to files in the background.



### Configuration

`FileLog` instances are configured with `FileLogSettings`, exposing following options:

| Option                       | Default value                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `FilePath`                   | `logs/log`                        | <p>Path to the log file. If rolling is enabled, this path serves as a base path and gets combined with various suffixes determined by the rolling strategy.</p><p></p><p>Position of the rolling suffix can be customized by inserting a special <code>{RollingSuffix}</code> placeholder somewhere in the file name.</p><p></p><p>This path is interpreted as relative to current working directory, though absolute paths are supported too.</p><p></p><p>File path is not allowed to point to a directory. </p> |
| `OutputTemplate`             | `OutputTemplate.Default`          | [Output template](../concepts/formatting/output-templates.md) to render log events with.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `FormatProvider`             | `null`                            | An optional format provider used when applying custom [format specifiers](../concepts/formatting/format-specifiers.md).                                                                                                                                                                                                                                                                                                                                                                                            |
| `FileOpenMode`               | `Append`                          | Specifies the way to treat an existing log file: append or rewrite.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `RollingStrategy.Type`       | `None`                            | Type of rolling strategy. Possible values are `None`, `ByTime`, `BySize` and `Hybrid`.                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `RollingStrategy.Period`     | `Day`                             | Period of switching to the next file when using `ByTime` or `Hybrid` rolling strategies. Possible values are `Day`, `Hour`, `Minute` and `Second`.                                                                                                                                                                                                                                                                                                                                                                 |
| `RollingStrategy.MaxSize`    | `1073741824`                      | Size threshold for switching to the next file when using `BySize` or `Hybrid` rolling strategies, specified in bytes.                                                                                                                                                                                                                                                                                                                                                                                              |
| `RollingStrategy.MaxFiles`   | `5`                               | <p>The number of most recent files to keep when using a rolling strategy: older files are automatically removed. Specify zero value to avoid removing old files. </p><p><strong>To avoid bringing down app with runaway disk space only the most recent <code>5</code> files are stored by default.</strong></p>                                                                                                                                                                                                   |
| `Encoding`                   | `UTF8`                            | Produced file's encoding.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `OutputBufferSize`           | `65536`                           | File stream buffer size, specified in bytes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `EnabledLogLevels`           | `Debug, Info, Warn, Error, Fatal` | A list of enabled log levels.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `EventsQueueCapacity`        | `50000`                           | Capacity of the internal log events queue.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `FileSettingsUpdateCooldown` | `1 second`                        | Cooldown for enforcing file-related settings (file path, rolling strategy, etc). This means that when conditions are met to switch to the next part of log file or reopen the file with another name/options due to change in settings, the switching may be delayed for up to value of this option.                                                                                                                                                                                                               |

All of these parameters are optional.

Most of listed options support dynamic reconfiguration when a constructor with `Func<FileLogSettings>` is used and provided delegate returns different instances of `FileLogSettings`. `FileLog` will react to these changes by either reopening the file, switching to a new file or simply using the new values where applicable.

The only notable exception to this rule is the `EventsQueueCapacity` option: it has a per-file scope and can't be changed dynamically.



### Usage tips

*   Keep in mind that log messages are written to files in the background. Use `Flush` or `FlushAsync` methods of `FileLog` to ensure that all logged events have been actually written at any given moment.


*   Remember to dispose of `FileLog` instances when they are no longer needed in order to close file handles. `Dispose` method also flushes all remaining messages before closing the file.


*   Internal queue with limited capacity implies that log messages may be lost in the event of overflow (see [guarantees section](../guarantees.md) for more on this topic). Use `EventsLost` property of a single `FileLog` instance or static `TotalEventsLost` property to check if any events have been discarded.


* If any log events are lost due to internal queue overflow, `FileLog` emits a special diagnostic message that looks like this:
  *   ```
      [FileLog] Buffer overflow. 100 log events were lost (events queue capacity = 50000).
      ```


*   When encountering any other severe internal error (such as inability to open the file), `FileLog` reports it to console.


* `FileLog` can be configured from any external source (such as a local settings file) with [Vostok.Configuration](https://vostok.gitbook.io/configuration/): just construct the log with a delegate that obtains `FileLogSettings` from a `ConfigurationProvider`.
