---
description: 'http://vostok.tools'
---

# Home

## Vostok.Logging

Logging is a means of tracking events that occur during the operation of some processes.  
Vostok.Logging like other libraries provides diagnostic logging to files, the console, and elsewhere.

The most important feature of Vostok.Logging is that the library doesn't affect the operation of the application. It means that app doesn't get exceptions to the library.

The second advantage of Vostok.Logging – [integration with other Vostok libraries](interaction-with-other-vostok-libraries.md).  For example, if you use Logging+Context, you can automatically add properties from context to logs.

## Features:

* **Structured logging** Log event consists of a timestamp, a log message, a saved exception and user-defined properties. The template of the log message containing placeholders to be filled with values from properties:

```csharp
ILog log = new ConsoleLog();
            
log.Info("{0}.Logging!", "Vostok");
log.Info("\"Flowers for {hero}\" {author}", new {author="Daniel Keyes", hero="Algernon"});
log.Error(new Exception("My exception"), "Something wrong");
log.Debug("{one} two {text}", 1, "3");

ConsoleLog.Flush();
```

* **Fully asynchronous** 
* **Flexible setting** 
* **Fast work** 
* \*\*\*\*[**Integration with Serilog and Log4Net**](integration-with-serilog-log4net/) ****You can try Vostok right now. There's no need to translate the whole system to the Vostok at once. Just use an adapter.

## Libraries

Vostok.Logging is a set of libraries:

| Library | Description |
| :--- | :--- |
| [Logging.Abstractions](https://github.com/vostok/logging.abstractions) | This library is a facade with core logging interfaces and models \([ILog](basics.md#ilog), [LogEvent](basics.md#logevent), [LogLevel](basics.md#loglevel)\) and a set of useful extensions. |
| [Logging.Console](https://github.com/vostok/logging.console) | This library is for a log which outputs events to console. Supports color-marked messages, uses lock-free queue for asynchronous message writing. |
| [Logging.File](https://github.com/vostok/logging.file) | This library is for a log which outputs events to file. Supports rolling-strategies for logs rotation, uses lock-free queue for asynchronous message writing, easy to configure from code and other sources. |
| [Logging.Context](https://github.com/vostok/logging.context) | Automatically adds info to log messages from background context. |
| [Logging.Formatting](https://github.com/vostok/logging.formatting) | Rendering messages and events to document. Can be used in your realisations of text logging. |
| [Logging.Log4Net](https://github.com/vostok/logging.log4net) | Represents an adapter between Vostok logging interfaces and log4net. |
| [Logging.Serilog](https://github.com/vostok/logging.serilog) | Represents an adapter between Vostok logging interfaces and Serilog. |
| [Logging.Hercules](https://github.com/vostok/logging.hercules) | This library is for a log which outputs events to Hercules. |





