---
description: Represents an adapter between Vostok logging interfaces and Serilog.
---

# Vostok.Logging.Serilog

If you have already using Serilog, but want to try Vostok.Logging, we have specific library Vostok.Logging.Serilog. It won't be necessary for you to rewrite all logging with it. Create an adapter, and you get Vostok's facade of the available log.

### First usage

Create an Serilog `ILogger`:

```csharp
var log = new LoggerConfiguration()
    .WriteTo.Console()
    .CreateLogger();
```

Create an adapter. We'll keep working with it:

```csharp
ILog adapter = new SerilogLog(log);
```

Let's try to work with it as with Vostok's ILog. Type any informational output message:

```csharp
adapter.Info("Easy Vostok");
```

We shall notice, that we treated it like Vostok's log, but we see Serilog's format on the console:

```aspnet
[13:36:38 INF] Easy Vostok
```

Why that is?  
We had Serilog's log. And then we created an adapter for treating it like Vostok's log. But all inside remained the same. Therefore, we see Serilog's format on the console.

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
We have Serilog's log which output events on console and we have Vostok's log which output events in the file.  
We need a single entry point for synchronous logging.  
Create a composite log for it. Pass fileLog и adapter in the composite.  
We passe the adapter because composite accept only Vostok's implementations.

```csharp
var composite = new CompositeLog(fileLog, adapter);

composite.Error("something wrong");

fileLog.Flush();
```

The result will be such Serilog's formate in output on the console and Vostok's formate in the file:

```aspnet
Console:
[14:10:22 INF] Easy Vostok
[13:36:39 ERR] Something wrong

File:
2018-11-08 13:36:39,119 ERROR Something wrong
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
[14:10:22 INF] Easy Vostok
[14:10:22 ERR] Something wrong
[14:10:22 INF] Show me text

File:
02:10:22 Something wrong   
02:10:22 Show me text 2 Service127 
```

Serilog log's settings remained. Log didn't process properties.   
We changed `FileLogSettings` and saw all the information about events and even properties in the file.

