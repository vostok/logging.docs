---
description: This page includes the basic concepts of Vostok.Logging
---

# Basics

Чтобы начать работать с библиотекой и понимать дальнейшие примеры, познакомимся с интерфесом восточных логов и с событиями. Посмотрим как создавать одни и другие.

### ILog

Represents a log. 

Чтобы создать стандартный лог, достаточно написать 1 строчку кода. В примере это будет лог, выводящий всю информацию на консоль. 

```csharp
Ilog logName = new ConsoleLog();
```

Подробнее о реализациях логах и их созданиии читайте в разделе [Implementations](implementations/).

### LogEvent

Event consists of a level, a timestamp, a log message, a saved exception and user-defined properties.

**Level**  
One of five level of the event: Debug, Info, Warn, Error, Fatal.

* **Debug** For verbose output. This log level should usually be ignored on production installations. ****
* **Info** For neutral messages.
* **Warn** For non-critical errors that don't interrupt the normal operation of the application.
* **Error** For unexpected errors that may require human attention.
* **Fatal** For critical errors that result in application shutdown.

**Timestamp**  
Represents the time when the event was created, rather then the time when it was written to a file or processed in any other way.

**Message template**  
The template of the log message containing placeholders to be filled with values from properties.  
Can be null for events containing only exception.

```csharp
log.Info("{0}.Logging!", "Vostok");
log.Info("Hello, {user}! Let's do {smth} today!", new {user="Alex", smth="nothing"});
log.Error(new Exception("Unicorn die"), "Happy Hippo");
```

**Properties**  
Contains various user-defined properties of the event.  
There are two kinds of properties:  
1. [Named properties](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments)  
2. [Positional parameters](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments)

**Exception**  
The error associated with this log event.

Попробуем создать различные события:

```csharp

```



