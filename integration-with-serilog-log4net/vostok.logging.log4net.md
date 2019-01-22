---
description: Represents an adapter between Vostok logging interfaces and log4net.
---

# Vostok.Logging.Log4net

If you're already using Log4net, but want to try Vostok.Logging, we have a special library Vostok.Logging.Log4net. You do not have to rewrite all logging. Create an adapter and you will get an Vostok facade from the available log.

### First usage

Create an Log4net `ILog`:

```csharp
private static readonly log4net.ILog log = LogManager.GetLogger
            (System.Reflection.MethodBase.GetCurrentMethod().DeclaringType);

static void Main(string[] args)
{
    var logRepository = LogManager.GetRepository(Assembly.GetEntryAssembly());
    XmlConfigurator.Configure(logRepository, new FileInfo("log4net.config"));
}
```

Create an adapter:

```csharp
 var adapter = new Log4netLog(log);
```

Work with it as with Vostok's ILog. Type any informational message:

```csharp
adapter.Info("test");
```

Result:

```aspnet
2018-11-09 11:59:06,776 INFO Log.Program - test
```

Why that is?  
There were Log4net logs. Then you created an adapter to handle as the Vostok log. But everything inside remained the same. So on the console you see the Log4net format.

### Example 1

Complement the example above.  
First of all, create a simple Vostok's file log:

```csharp
var fileLog = new FileLog(new FileLogSettings
{
    FilePath = "log.log"
});
```

Create a log that records information synchronously to the console and to a file.  
You have Log4net's log which output events on console and Vostok's log which output events in the file.  
A single entry point is required for synchronous entry.  
Create a composite log for it. Pass fileLog and adapter in the composite.  
The adapter is necessary because composite only accepts Vostok implementations.

```csharp
var composite = new CompositeLog(fileLog, adapter);

composite.Error("something wrong");

fileLog.Flush();
```

The result will be such Log4net's formate in output on the console and Vostok's formate in the file:

```aspnet
Console:
2018-11-09 12:02:34,209 INFO Log.Program - test
2018-11-09 12:02:34,304 ERROR Log.Program - something wrong

File:
2018-11-09 12:02:34,304 ERROR something wrong
```

### Example 2

Create an event with added properties. Pass it in `composite`:

```csharp
 var event2 = new LogEvent(LogLevel.Info, DateTimeOffset.Now, "Show me text")    
    .WithProperty("Priority", 2)    
    .WithProperty("Author", "Service127");
 
composite.Log(event2);
```

Additionally, configure `FileLog` to see added properties in the file:

```csharp
var fileLog = new FileLog(new FileLogSettings
{
    FilePath = "log.log",
    OutputTemplate = OutputTemplate.Parse("{TimeStamp:hh:mm:ss} {Message} {Priority} {Author} {Exception}{NewLine}")
});
```

The result will be such output on the console:

```aspnet
Console:
2018-11-09 12:03:35,169 INFO Log.Program - test
2018-11-09 12:03:35,288 ERROR Log.Program - something wrong
2018-11-09 12:03:35,280 INFO Log.Program - Show me text

File:
12:03:35 something wrong   
12:03:35 Show me text 2 Service127 
```

Log4net log's settings remained. Log didn't process properties.   
You changed `FileLogSettings` and saw all event information and even properties in the file.

