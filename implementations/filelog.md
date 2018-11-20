---
description: A log which outputs events to a file.
---

# FileLog

Include `Logging.File` library in project:

```csharp
using Vostok.Logging.File;
```

 An `ILog` is created using `FileLog`:

```csharp
var log = new FileLog(
    new FileLogSettings { FilePath = "log.txt" });
```

Create logs  
Use `Flush` or `FlushAsync` to ensure that logged events are written to file.

```csharp
log.Info("1");
log.Debug("2");
log.Warn("3");

FileLog.FlushAll();
```

Хорошо, у нас получилось записывать логи в файл. Попробуем теперь его настроить.

Поработаем с названием файла, в который собираемся записывать логи. Пусть название файла будет содержать текущее время:

```csharp
ILog flog = new FileLog(new FileLogSettings
{
    FilePath = Path.Combine($"{DateTime.Now:yyyy-MM-dd.HH-mm-ss}.log")     
});
```

Выберем уровни логирования. Сообщения только этих уровней будем записывать в файл:

```csharp
ILog flog = new FileLog(new FileLogSettings
{
    FilePath = Path.Combine($"{DateTime.Now:yyyy-MM-dd.HH-mm-ss}.log"),
    EnabledLogLevels = new [] {LogLevel.Error, LogLevel.Fatal},      
});
```

Изменим кодировку:

```csharp
ILog flog = new FileLog(new FileLogSettings
{
    FilePath = Path.Combine($"{DateTime.Now:yyyy-MM-dd.HH-mm-ss}.log"),
    EnabledLogLevels = new [] {LogLevel.Error, LogLevel.Fatal},
    Encoding = Encoding.BigEndianUnicode
});
```

Примеры использования этих и других настроек смотрите в разделе [Advanced Usage](../advanced-usage.md).

### Configurations

Выше мы рассмотрели несколько примеров настройки файлового лога из кода. Но это не единственный способ как можно построить этот процесс.

There are three ways to configure Vostok's FileLog:

* Create settings file;
* Set settings provider;
* Use Vostok.Configuration\(ссылка на отсутствующую документацию\)

```csharp
// configure from code — settings instance
var log1 = new FileLog(new FileLogSettings());

// configure from code — settings instance provider
var log2 = new FileLog(() => new FileLogSettings());

// configure from file
var log3 = new FileLog(new JsonFileSource("log3.json"));
```

Пример конфигурационного файла:

```text
*тут я не умею, наверное*
```

### Settings

Ниже всё, что можно настроить в файловом логе:

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
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

