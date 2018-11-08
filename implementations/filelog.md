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

* \*\*\*\*[**FilePath**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**OutputTemplate**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**FormatProvider**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**FileOpenMode**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**RollingStrategy**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**Encoding**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**OutputBufferSize**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**EnabledLogLevels**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**EventsQueueCapacity**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**EventsBufferCapacity**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)
* [**FileSettingsUpdateCooldown**](https://github.com/vostok/logging.file/blob/master/Vostok.Logging.File/Configuration/FileLogSettings.cs)\*\*\*\*



