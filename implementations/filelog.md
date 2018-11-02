---
description: A log which outputs events to a file.
---

# FileLog

файловый лог блаблабла–блаблаблабла

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



```text

```





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















//

The implementation is asynchronous and thread-safe: logged messages are not immediately rendered and written to file. Instead, they are added to a lock-free queue which is processed by a background worker.  
The capacity of the queue can be changed in settings if a settings provider is used. In case of a queue overflow some events may be dropped.

Use `Flush` or `FlushAsync` to ensure that logged events are written to file.  
Use `EventsLost` counter to see how many events were lost due to queue overflow.  
Remember to Dispose a FileLog instance when you no longer need it to close the file handle.  
Log method never throws exceptions. On the other hand, `Flush` and `FlushAsync` may do so.

