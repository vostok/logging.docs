---
description: Represents an adapter between Vostok logging interfaces and log4net.
---

# Vostok.Logging.Log4net

If you have already using Log4net, but want to try Vostok.Logging, we have specific library Vostok.Logging.Log4net. It won't be necessary for you to rewrite all logging with it. Create an adapter, and you get Vostok's facade of the available log.

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

Create an adapter. We'll keep working with it:

```csharp
 var adapter = new Log4netLog(log);
```

Let's try to work with it as with Vostok's ILog. Type any informational output message:

```csharp
adapter.Info("test");
```

We shall notice, that we treated it like Vostok's log, but we see Log4net's format on the console:

```aspnet
2018-11-09 11:59:06,776 INFO Log.Program - test
```

Why that is?  
We had Log4net's log. And then we created an adapter for treating it like Vostok's log. But all inside remained the same. Therefore, we see Log4net's format on the console.

### Example 1

Try to do something slightly more complicated. Let's complement the example above.  
First of all, create a simple Vostok's file log:

```csharp
var fileLog = new FileLog(new FileLogSettings
{
    FilePath = "log.log"
});
```

We would create a log which synchronous logging on the console and in a file.  
We have Log4net's log which output events on console and we have Vostok's log which output events in the file.  
We need a single entry point for synchronous logging.  
Create a composite log for it. Pass fileLog и adapter in the composite.  
We passe the adapter because composite accept only Vostok's implementations.

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

Let's a few more complicate the code above and see what's going.  
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
We changed `FileLogSettings` and saw all the information about events and even properties in the file.

