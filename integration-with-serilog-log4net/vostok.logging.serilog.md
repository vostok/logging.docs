---
description: Represents an adapter between Vostok logging interfaces and Serilog.
---

# Vostok.Logging.Serilog

If you're already using Serilog, but want to try Vostok.Logging, we have a special library Vostok.Logging.Serilog. You do not have to rewrite all logging. Create an adapter and you will get an Vostok facade from the available log.

### First usage

Create an Serilog `ILogger`:

```csharp
var log = new LoggerConfiguration()
    .WriteTo.Console()
    .CreateLogger();
```

Create an adapter:

{% tabs %}
{% tab title="" %}
```csharp
ILog adapter = new SerilogLog(log);
```
{% endtab %}
{% endtabs %}

Work with it as with Vostok's ILog. Type any informational message:

```csharp
adapter.Info("Easy Vostok");
```

Result:

```aspnet
[13:36:38 INF] Easy Vostok
```

Why? There were Serilog logs. Then you created an adapter to handle as the Vostok log. But everything inside remained the same. So on the console you see the Serilog format.

### Example 1

Try to do something slightly more complicated. Complement the example above.  
First of all, create a simple Vostok's file log:

```csharp
var fileLog = new FileLog(new FileLogSettings
{
    FilePath = "log.log"
});
```

Create a log that records information synchronously to the console and to a file.  
You have Serilog's log which output events on console and Vostok's log which output events in the file.  
A single entry point is required for synchronous entry.  
Create a composite log for it. Pass fileLog and adapter in the composite.  
The adapter is necessary because composite only accepts Vostok implementations.

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

Serilog log's settings remained. Log didn't process properties. You changed the`FileLogSettings` and saw all event information and even properties in the file.

