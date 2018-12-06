# Quick Start

## Installing from NuGet

Dependencies: .NETStandart 2.0

```aspnet
PM> Install-Package Vostok.Logging.Abstractions -Version 0.1.1-pre000045
PM> Install-Package Vostok.Logging.Console -Version 0.1.3-pre000069
```

Browse the [Vostok.Logging tag on NuGet](https://www.nuget.org/packages?q=Vostok.Logging) to see more packages.

## SetUp

Let's try Vostok and write a simple program. We'll [Console Log](implementations/consolelog.md)-work.

Include Vostok libraries in project:

```csharp
using Vostok.Logging.Abstractions;
using Vostok.Logging.Console;
```

Create a log using a `ConsoleLog()`.   
Create Informational message with text "_Hello!_ ".  
To make everything work and we have seen the text on the console add `ConsoleLog.Flush()` in your file:

```csharp
Ilog log = new ConsoleLog();
            
log.Info("Hello, {user}!", "I-430");
ConsoleLog.Flush();
```

Result:

```aspnet
2018-11-06 16:37:00,193 INFO  Hello, I-430!
```

## First usage

Let's try to use `ConsoleLog` in a simple task.  
Build a situation in which `System.NullReferenceException` happens.  
We'll log all of the operations. Try to convert null to int. Rather than crash, show the message "Something wrong ":

```csharp
ILog log = new ConsoleLog();
                       
log.Info("test");

object o2 = null;  
try  
{  
    log.Debug("{check}");
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

We got the full information about time and consistency of operation from logging.  
Logging will help you localise a problem if service is massive.

