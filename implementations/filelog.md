---
description: A log which outputs events to a file.
---

# FileLog

### Set Up

Include `Logging.File` library in project:

```csharp
using Vostok.Logging.File;
```

 An `ILog` is created using `FileLog`:

```csharp
var log = new FileLog(
    new FileLogSettings { FilePath = "log.txt" });
```

Create logs:

```csharp
log.Info("1");
log.Debug("2");
log.Warn("3");
```

Use `Flush` or `FlushAsync` to ensure that logged events are written to file:

```csharp
FileLog.FlushAll();
```

Well, we managed to write logs to file. Let's try to configure log.

Change filename. Let it will contain the current time:

```csharp
ILog flog = new FileLog(new FileLogSettings
{
    FilePath = Path.Combine($"{DateTime.Now:yyyy-MM-dd.HH-mm-ss}.log")     
});
```

Choose enabled log levels. We'll write in the file only these levels' messages:

```csharp
ILog flog = new FileLog(new FileLogSettings
{
    FilePath = Path.Combine($"{DateTime.Now:yyyy-MM-dd.HH-mm-ss}.log"),
    EnabledLogLevels = new [] {LogLevel.Error, LogLevel.Fatal},      
});
```

Change encoding:

```csharp
ILog flog = new FileLog(new FileLogSettings
{
    FilePath = Path.Combine($"{DateTime.Now:yyyy-MM-dd.HH-mm-ss}.log"),
    EnabledLogLevels = new [] {LogLevel.Error, LogLevel.Fatal},
    Encoding = Encoding.BigEndianUnicode
});
```

See the section about [Advanced Usage](../advanced-usage/) for samples of settings usage.

### Configurations

Above is an example of how to configure a FileLog from code. However, this is not the only way how we can build this process.

There are two ways to configure Vostok's FileLog:

* create settings file;
* set settings provider.

```csharp
// configure from code — settings instance
var log1 = new FileLog(new FileLogSettings());

// configure from code — settings instance provider
var log2 = new FileLog(() => new FileLogSettings());

// configure from file
var log3 = new FileLog(new JsonFileSource("log3.json"));
```

Sample configuration file :

```text
*тут я не умею, наверное*
```

### Settings

These parameters are adjusted in `FileLogSettings`:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><b></b>
        </p>
        <p><b></b><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>FilePath</b></a>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>Path to the log file</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>OutputTemplate</b></a>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>Used to render log messages</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>FormatProvider</b></a>
        </p>
      </td>
      <td style="text-align:left">If specified, this IFormatProvider will be used when formatting log property
        values</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>FileOpenMode</b></a>
        </p>
      </td>
      <td style="text-align:left">Specifies the way to treat an existing log file: append (default) or rewrite</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>RollingStrategy</b></a>
        </p>
      </td>
      <td style="text-align:left">An optional rolling strategy (disabled by default)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>Encoding</b></a>
        </p>
      </td>
      <td style="text-align:left">Output text encoding (UTF-8 by default)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>OutputBufferSize</b></a>
        </p>
      </td>
      <td style="text-align:left">Output buffer size, in bytes (64K by default)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>EnabledLogLevels</b></a>
        </p>
      </td>
      <td style="text-align:left">A whitelist of enabled LogLevels</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>EventsQueueCapacity</b></a>
        </p>
      </td>
      <td style="text-align:left">Capacity of the internal log events queue</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>EventsBufferCapacity</b></a>
        </p>
      </td>
      <td style="text-align:left">Specifies how many log events are processed in one iteration for each
        file</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs"><b>FileSettingsUpdateCooldown</b></a><b></b>
        </p>
      </td>
      <td style="text-align:left">Cooldown for enforcing file-related settings (name, rolling strategy,
        buffer size, etc.)</td>
    </tr>
  </tbody>
</table>

