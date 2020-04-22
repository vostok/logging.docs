# File log

**Location**: [file module](../modules/file.md).

```csharp
var fileLog = new FileLog(new FileLogSettings());
var dynamicallyConfiguredLog = new FileLog(() => ObtainSettings());
```



### Features

* Customizable [output templates](../concepts/formatting/output-templates.md).
* Customizable rolling strategies:
  * By size \(roll over to a new file when current one reaches given size\)
  * By time \(roll over to a new file every second/minute/hour/day\)
  * Hybrid \(both by size and time\)
  * Automatic cleanup of stale files
* Multiplexing: multiple `FileLog` instances inside a single process may write to the same file without performance penalties.
* `Log` method is nonblocking: log events are placed into an internal queue, buffered and efficiently written to files in the background.



### Configuration

`FileLog` instances are configured with `FileLogSettings`, exposing following options:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Default value</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>FilePath</code>
      </td>
      <td style="text-align:left"><code>logs/log</code>
      </td>
      <td style="text-align:left">
        <p>Path to the log file. If rolling is enabled, this path serves as a base
          path and gets combined with various suffixes determined by the rolling
          strategy.</p>
        <p></p>
        <p>Position of the rolling suffix can be customized by inserting a special <code>{RollingSuffix}</code> placeholder
          somewhere in the file name.</p>
        <p></p>
        <p>This path is interpreted as relative to current working directory, though
          absolute paths are supported too.</p>
        <p></p>
        <p>File path is not allowed to point to a directory.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>OutputTemplate</code>
      </td>
      <td style="text-align:left"><code>OutputTemplate.Default</code>
      </td>
      <td style="text-align:left"><a href="../concepts/formatting/output-templates.md">Output template</a> to
        render log events with.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FormatProvider</code>
      </td>
      <td style="text-align:left"><code>null</code>
      </td>
      <td style="text-align:left">An optional format provider used when applying custom <a href="../concepts/formatting/format-specifiers.md">format specifiers</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FileOpenMode</code>
      </td>
      <td style="text-align:left"><code>Append</code>
      </td>
      <td style="text-align:left">Specifies the way to treat an existing log file: append or rewrite.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>RollingStrategy.Type</code>
      </td>
      <td style="text-align:left"><code>None</code>
      </td>
      <td style="text-align:left">Type of rolling strategy. Possible values are <code>None</code>, <code>ByTime</code>, <code>BySize</code> and <code>Hybrid</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>RollingStrategy.Period</code>
      </td>
      <td style="text-align:left"><code>Day</code>
      </td>
      <td style="text-align:left">Period of switching to the next file when using <code>ByTime</code> or <code>Hybrid</code> rolling
        strategies. Possible values are <code>Day</code>, <code>Hour</code>, <code>Minute</code> and <code>Second</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>RollingStrategy.MaxSize</code>
      </td>
      <td style="text-align:left"><code>1073741824</code>
      </td>
      <td style="text-align:left">Size threshold for switching to the next file when using <code>BySize</code> or <code>Hybrid</code> rolling
        strategies, specified in bytes.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>RollingStrategy.MaxFiles</code>
      </td>
      <td style="text-align:left"><code>5</code>
      </td>
      <td style="text-align:left">The number of most recent files to keep when using a rolling strategy:
        older files are automatically removed. Specify zero value to avoid removing
        old files.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>Encoding</code>
      </td>
      <td style="text-align:left"><code>UTF8</code>
      </td>
      <td style="text-align:left">Produced file&apos;s encoding.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>OutputBufferSize</code>
      </td>
      <td style="text-align:left"><code>65536</code>
      </td>
      <td style="text-align:left">File stream buffer size, specified in bytes.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>EnabledLogLevels</code>
      </td>
      <td style="text-align:left"><code>Debug, Info, Warn, Error, Fatal</code>
      </td>
      <td style="text-align:left">A list of enabled log levels.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>EventsQueueCapacity</code>
      </td>
      <td style="text-align:left"><code>50000</code>
      </td>
      <td style="text-align:left">Capacity of the internal log events queue.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FileSettingsUpdateCooldown</code>
      </td>
      <td style="text-align:left"><code>1 second</code>
      </td>
      <td style="text-align:left">Cooldown for enforcing file-related settings (file path, rolling strategy,
        etc). This means that when conditions are met to switch to the next part
        of log file or reopen the file with another name/options due to change
        in settings, the switching may be delayed for up to value of this option.</td>
    </tr>
  </tbody>
</table>All of these parameters are optional.

Most of listed options support dynamic reconfiguration when a constructor with `Func<FileLogSettings>` is used and provided delegate returns different instances of `FileLogSettings`. `FileLog` will react to these changes by either reopening the file, switching to a new file or simply using the new values where applicable.

The only notable exception to this rule is the `EventsQueueCapacity` option: it has a per-file scope and can't be changed dynamically.



### Usage tips

* Keep in mind that log messages are written to files in the background. Use `Flush` or `FlushAsync` methods of `FileLog` to ensure that all logged events have been actually written at any given moment.

* Remember to dispose of `FileLog` instances when they are no longer needed in order to close file handles. `Dispose` method also flushes all remaining messages before closing the file.

* Internal queue with limited capacity implies that log messages may be lost in the event of overflow \(see [guarantees section](../guarantees.md) for more on this topic\). Use `EventsLost` property of a single `FileLog` instance or static `TotalEventsLost` property to check if any events have been discarded.

* If any log events are lost due to internal queue overflow, `FileLog` emits a special diagnostic message that looks like this:
  * ```text
    [FileLog] Buffer overflow. 100 log events were lost (events queue capacity = 50000).
    ```
* When encountering any other severe internal error \(such as inability to open the file\), `FileLog` reports it to console.

* `FileLog` can be configured from any external source \(such as a local settings file\) with [Vostok.Configuration](https://vostok.gitbook.io/configuration/): just construct the log with a delegate that obtains `FileLogSettings` from a `ConfigurationProvider`.

