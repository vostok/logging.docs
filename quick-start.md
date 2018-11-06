# Quick Start

## Installing from NuGet

Dependencies: .NETStandart 2.0

```aspnet
PM> Install-Package Vostok.Logging.Abstractions -Version 0.1.1-pre000045
PM> Install-Package Vostok.Logging.Console -Version 0.1.3-pre000069
```

Browse the [Vostok.Logging tag on NuGet](https://www.nuget.org/packages?q=Vostok.Logging) to see more packages.

##  SetUp

Let's try Vostok and write a simple program. Работать будем с [ConsoleLog](implementations/consolelog.md).

Include Vostok libraries in project:

```csharp
using Vostok.Logging.Abstractions;
using Vostok.Logging.Console;
```

Create a log using a `ConsoleLog()`.   
Создадим информационное сообщение с тексом "_Hello!_ ".  
Чтобы всё заработало и мы увидели текст на консоли, добавим магическую строчку  
`ConsoleLog.Flush();`

```csharp
Ilog log = new ConsoleLog();
            
log.Info("Hello!");
ConsoleLog.Flush();
```

Result:

```aspnet
2018-11-06 16:37:00,193 INFO  Hello!
```

## First usage

Попробуем использовать консольный лог в простой задаче  
Построим ситуацию, в которой возникает `System.NullReferenceException` .  
Попробуем выполнить каст null to int. Будем логировать все действия. Вместо того, чтобы упасть, выведем сообщение "_Something wrong_ " :

```csharp
ILog log = new ConsoleLog();
                       
log.Info("test");

object o2 = null;  
try  
{  
    log.Debug("check");
    int i2 = (int)o2; 
}
catch(Exception e)
{
    log.Error("something wrong");
}

ConsoleLog.Flush();
```

Result:

```aspnet
2018-10-27 22:18:51,593 INFO  test
2018-10-27 22:18:51,636 DEBUG check
2018-10-27 22:18:51,638 ERROR something wrong
```

С помощью логирования мы получили полную информацию что и когда произошло.  
Если сервис большой, логирование поможет локализовать проблему и возможно найти причинно-следственные связи.

