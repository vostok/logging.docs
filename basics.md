---
description: This page includes the basic concepts of Vostok.Logging
---

# Basics

### [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs)

Represents a log.   
Implementations are expected to be thread-safe and never throw exceptions in any method.

`ILog` has three methods:

| Method | Description |
| :--- | :--- |
| Log | Logs the given `LogEvent`. |
| IsEnabledFor | Returns whether the current log is configured to log events of the given `LogLevel`. |
| ForContext | Returns a copy of the log operating in the given source context. |

### [LogEvent](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/LogEvent.cs)

Event consists of a level, a timestamp, a log message, a saved exception and user-defined properties.

\*\*\*\*[**Level**](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/LogLevel.cs)  
****One of five level of the event:

* **Debug** For verbose output.
* **Info** For neutral messages.
* **Warn** For non-critical errors that don't interrupt the normal operation of the application.
* **Error** For unexpected errors that may require human attention.
* **Fatal** For critical errors that result in application shutdown.

**Timestamp**  
Represents the time when the event was created.

**Message template**  
The template of the log message containing placeholders to be filled with values from.  
A few examples can be found [here](syntax.md#message-template).

**Properties**  
Contains various user-defined properties of the event.

**Exception**  
The error associated with this log event.

## 

For your convenience, we recommend using extensions instead of methog `Log` .  




























```csharp
LogEvent event1 = new LogEvent(LogLevel.Debug, DateTimeOffset.Now, "Just do it");

var event2 = new LogEvent(LogLevel.Info, DateTimeOffset.Now, "Show me text")
    .WithProperty("Priority", 2)
    .WithProperty("Author", "Service127");

var event3 = event2.WithoutProperty("Author");
    
var event4 = new LogEvent(LogLevel.Error, DateTimeOffset.Now, "", new Exception("my Exception"))
    .WithPropertyIfAbsent("Priority", 0);
    
var consoleLog = new ConsoleLog(new ConsoleLogSettings
{
    OutputTemplate = OutputTemplate.Parse("{TimeStamp:hh:mm:ss} {Message} {Priority} {Author} {Exception}{NewLine}")
});

var log = new CompositeLog(consoleLog);
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



