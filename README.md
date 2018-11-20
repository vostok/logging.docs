---
description: 'http://vostok.tools'
---

# Home

## Vostok.Logging

Logging is a means of tracking events that occur during the operation of some processes.  
Vostok.Logging like other libraries provides diagnostic logging to files, the console, and elsewhere.

## Libraries

Vostok.Logging is a set of libraries. 

| Library | Description |
| :--- | :--- |
| [Logging.Abstractions](https://github.com/vostok/logging.abstractions) | This library is a facade with core logging interfaces and models \([ILog](basics.md#ilog), [LogEvent](basics.md#logevent), [LogLevel](basics.md#loglevel)\) and a set of useful extensions. |
| [Logging.Console](https://github.com/vostok/logging.console) | This library is for a log which outputs events to console. Supports color-marked messages, uses lock-free queue for asynchronous message writing. |
| [Logging.File](https://github.com/vostok/logging.file) | This library is for a log which outputs events to file. Supports rolling-strategies for logs rotation, uses lock-free queue for asynchronous message writing, easy to configure from code and other sources. |
| [Logging.Context](https://github.com/vostok/logging.context) | Automatically adds info to log messages from background context. |
| [Logging.Formatting](https://github.com/vostok/logging.formatting) | Rendering messages and events to document. Can be used in your realisations of text logging. |
| [Logging.Log4Net](https://github.com/vostok/logging.log4net) | Represents an adapter between Vostok logging interfaces and log4net. |
| [Logging.Serilog](https://github.com/vostok/logging.serilog) | Represents an adapter between Vostok logging interfaces and Serilog. |
| [Logging.Hercules](https://github.com/vostok/logging.hercules) |  |

## Features:

* **Structured logging** Log event consists of a timestamp, a log message, a saved exception and user-defined properties. 
* **Fully asynchronous** 
* **Flexible setting** 
* **Fast work** 
* \*\*\*\*[**Integration with Serilog and Log4Net**](integration-with-serilog-log4net/) ****You can try Vostok right now. No need to translate the whole system to the Vostok at once. Just use an adapter. 

But Vostok is not just one library it's a toolbox. If you use several Vostok libraries, your profit is in good integration.  
No worries about compatibility and other libraries.



