---
description: 'http://vostok.tools'
---

# Initial page

## Vostok.Logging

Logging is a means of tracking events that occur during the operation of some processes.  
Vostok.Logging like other libraries provides diagnostic logging to files, the console, and elsewhere.

### Features:

* **Structured logging** Log event consists of a timestamp, a log message, a saved exception and user-defined properties.

```csharp
var @event = new LogEvent(LogLevel.Info, DateTimeOffset.Now, "Hello, Vostok!");
var template = OutputTemplate.Parse("{Level} {Message}");
var result = LogEventFormatter.Format(@event, template);

```

* **Fully asynchronous** 
* **Flexible setting** You can customize your logs. Examples are [here](advanced-usage/). 
* **Fast work** Similar messages ~ 23 000 messages/sec Different ~ 8 500 – 16 000 messages/sec 
* \*\*\*\*[**Integration with Serilog and Log4Net**](integration-with-serilog-log4net/) ****You can try Vostok right now. No need to translate the whole system to the Vostok at once. Just use an adapter. 

But Vostok is not just one library it's a toolbox. If you use several Vostok libraries, your profit is in good integration.  
No worries about compatibility and other libraries.



