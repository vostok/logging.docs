---
description: A log which outputs events to a file.
---

# FileLog

The implementation is asynchronous and thread-safe: logged messages are not immediately rendered and written to file. Instead, they are added to a lock-free queue which is processed by a background worker.  
The capacity of the queue can be changed in settings if a settings provider is used. In case of a queue overflow some events may be dropped.

Use `Flush` or `FlushAsync` to ensure that logged events are written to file.  
Use `EventsLost` counter to see how many events were lost due to queue overflow.  
Remember to Dispose a FileLog instance when you no longer need it to close the file handle.  
Log method never throws exceptions. On the other hand, `Flush` and `FlushAsync` may do so.

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

```csharp
log.Info("1");
log.Debug("2");
log.Warn("3");

FileLog.FlushAll();
```

Хорошо, у нас получилось записывать логи в файл. Попробуем теперь его настроить.  
Для начала сделаем минимальный уровень логирования. Пусть это будет Warn:

```text

```

Остальные примеры настройки восточных логов смотрите в разделе [Advanced Usage](../advanced-usage.md).

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

### 

