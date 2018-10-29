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

Create a log using a `ConsoleLog()` :

```csharp
Ilog log = new ConsoleLog();
            
log.Info("Hello!");
ConsoleLog.Flush();
```

Result:

```csharp
2018-09-11 13:45:00,162 INFO Hello!
```

## First usage

Попробуем использовать консольный лог в простой задаче

```csharp
ILog log2 = new ConsoleLog();
                       
log2.Info("test");

object o2 = null;  
try  
{  
    log2.Debug("check");
    int i2 = (int)o2; 
}
catch(Exception e)
{
    log2.Error("something wrong");
}

ConsoleLog.Flush();
Console.ReadLine();
```

Result:

```csharp
2018-10-27 22:18:51,593 INFO  test
2018-10-27 22:18:51,636 DEBUG check
2018-10-27 22:18:51,638 ERROR something wrong
```



