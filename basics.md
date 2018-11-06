---
description: This page includes the basic concepts of Vostok.Logging
---

# Basics

Для работы с библиотекой и понимания дальнейших примеров, познакомимся с событиями и интерфейсом восточных логов . Посмотрим как создавать одни и другие.

### ILog

Represents a log. 

Чтобы создать стандартный лог, достаточно написать 1 строчку кода.  
В примере это будет лог, выводящий всю информацию на консоль\*. 

```csharp
Ilog logName = new ConsoleLog();
```

\*Подробнее о реализациях логах и их созданиии читайте в разделе [Implementations](implementations/).

### LogEvent

Event consists of a level, a timestamp, a log message, a saved exception and user-defined properties.

**Level**  
One of five level of the event:

* **Debug** For verbose output. This log level should usually be ignored on production installations. ****
* **Info** For neutral messages.
* **Warn** For non-critical errors that don't interrupt the normal operation of the application.
* **Error** For unexpected errors that may require human attention.
* **Fatal** For critical errors that result in application shutdown.

**Timestamp**  
Represents the time when the event was created.

**Message**  
Текст, описание события

**Properties**  
Contains various user-defined properties of the event.

**Exception**  
The error associated with this log event.

Попробуем создать различные события:

```csharp
LogEvent event1 = new LogEvent(LogLevel.Debug, DateTimeOffset.Now, "Just do it");

var event2 = new LogEvent(LogLevel.Info, DateTimeOffset.Now, "Show me text")
    .WithProperty("Priority", 2)
    .WithProperty("Author", "Service127");

var event3 = event2.WithoutProperty("Author");
    
var event4 = new LogEvent(LogLevel.Error, DateTimeOffset.Now, "", new Exception("my Exception"))
    .WithPropertyIfAbsent("Priority", 0);
    
var clog = new ConsoleLog(new ConsoleLogSettings
{
    OutputTemplate = OutputTemplate.Parse("{TimeStamp:hh:mm:ss} {Message} {Priority} {Author} {Exception}{NewLine}")
});

var log = new CompositeLog(clog);
log.Log(event1);
log.Log(event2);
log.Log(event3);
log.Log(event4);

ConsoleLog.Flush();
```

Result:

```aspnet
02:47:08 Just do it   
02:47:08 Show me text 2 Service127 
02:47:08 Show me text 2  
02:47:08  0  System.Exception: my Exception
```

### **Message Template**

The template of the log message containing placeholders to be filled with values from properties.  
Попробуем 

```csharp
log.Info("{0}.Logging!", "Vostok");
log.Info("Hello, {user}! Let's do {smth} today!", new {user="Alex", smth="nothing"});
log.Error(new Exception("Unicorn die"), "Happy Hippo");
```



