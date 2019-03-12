# Console log

**Location**: [console](../modules/console.md) module.

```csharp
var consoleLog = new ConsoleLog();
var configuredConsoleLog = new ConsoleLog(new ConsoleLogSettings());
```



### Features

* Customizable [output templates](../concepts/formatting/output-templates.md).
* Customizable per-level message colors.
* `Log` method is nonblocking: log events are placed into an internal queue, grouped into batches and efficiently written to console output stream in the background.



### Configuration

Here's what `ConsoleLogSettings` have to offer:

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
      <td style="text-align:left"><code>ColorsEnabled</code>
      </td>
      <td style="text-align:left"><code>false</code>
      </td>
      <td style="text-align:left">Enables/disables coloring of log messages.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ColorMapping</code>
      </td>
      <td style="text-align:left">
        <p><code>Debug</code> =&gt; <code>Gray</code>,</p>
        <p><code>Info</code> =&gt; <code>White</code>,</p>
        <p><code>Warn</code> =&gt; <code>Yellow</code>,</p>
        <p><code>Error</code> =&gt; <code>Red</code>,</p>
        <p><code>Fatal</code> =&gt; <code>DarkRed</code>
        </p>
      </td>
      <td style="text-align:left">Provides a mapping from log levels to console colors.</td>
    </tr>
  </tbody>
</table>All configuration parameters are optional.



### Global configuration

There's also static global configuration that affects all `ConsoleLog` instances in the application. It is accessed as follows:

```csharp
ConsoleLog.UpdateGlobalSettings(new ConsoleLogGlobalSettings());
```

This configuration exposes following parameters worth mentioning:

| Option | Default value | Description |
| :--- | :--- | :--- |
| `EventsQueueCapacity` | `50000` | Maximum count of log events in internal queue. |
| `OutputBufferSize` | `65536` | Size of the buffer used when writing log messages to console output stream \(in bytes\). |

Note that changes in these global configuration parameters only take effect if performed before any actual logging.



### Usage tips

* Keep in mind that log messages are rendered in the background. Use `Flush` or `FlushAsync` methods of `ConsoleLog` to ensure that all logged events have been written to console when the application shuts down.

* Internal queue with limited capacity implies that log messages may be lost in the event of overflow \(see [guarantees section](../guarantees.md) for more on this topic\). Use `EventsLost` property of a single `ConsoleLog` instance or static `TotalEventsLost` property to check if any events have been discarded.



### Synchronous version

There are certain scenarios where it's not feasible to use an asynchronous log, such as logging in unit tests or simple console utilities. These use cases are better served by an alternative synchronous implementation that writes to console immediately in `Log` method:

```csharp
var synchronousLog = new SynchronousConsoleLog();
```

It's performance is vastly inferior to that of `ConsoleLog` due to lack of buffering, but it removes the need to flush and works well in test environments where `Console.Out` cannot be safely cached.

