# Home

## Vostok.Logging

Vostok.Logging is a set of [libraries](./#libraries). Like other popular libraries \([Serilog](https://serilog.net), [Log4net](https://logging.apache.org/log4net/) etc.\) it provides diagnostic logging to files, the console, and elsewhere.

Vostok.Logging is not a monolith. The library consists of parts: facade and implementations.

## Peculiarities:

* Efficient built-in [implementations](implementations/) out of the box; 
* Logging is tightly integrated into the Vostok ecosystem. If you use the entire Vostok or multiple libraries, you don't need to worry about integration. Read more in the section [integration with other Vostok libraries](interaction-with-other-vostok-libraries.md).

## Features:

* **Structured logging** In the Vostok.Logging as in Serilog logs are structured. You can render user-defined properties. Learn more about template syntax [here](syntax.md). 
* **Fully asynchronous** Calling the `Log` method can't lock the app. 
* **Fast work** \*proof\* 
* \*\*\*\*[**Integration with Serilog and Log4Net**](integration-with-serilog-log4net/) ****If you are already using Serilog or Log4net, create an adapter and you'll get the Vostok facade from the available log.

## Libraries

| Library | Description |
| :--- | :--- |
| [Logging.Abstractions](https://github.com/vostok/logging.abstractions) | This library is a facade with core logging interfaces and models \([ILog](basics.md#ilog), [LogEvent](basics.md#logevent), [LogLevel](basics.md#loglevel)\) and a set of useful extensions. |
| [Logging.Console](https://github.com/vostok/logging.console) | This library is for a log which outputs events to console. Supports color-marked messages, uses lock-free queue for asynchronous message writing. |
| [Logging.File](https://github.com/vostok/logging.file) | This library is for a log which outputs events to file. Supports rolling-strategies for logs rotation, uses lock-free queue for asynchronous message writing, easy to configure from code and other sources. |
| [Logging.Context](https://github.com/vostok/logging.context) | Automatically embeds contextual information in the log message. |
| [Logging.Formatting](https://github.com/vostok/logging.formatting) | This library responsible for rendering messages and log events to text. Used in any standalone text-based log implementation. |
| [Logging.Log4Net](https://github.com/vostok/logging.log4net) | Represents an adapter between Vostok logging interfaces and log4net. |
| [Logging.Serilog](https://github.com/vostok/logging.serilog) | Represents an adapter between Vostok logging interfaces and Serilog. |
| [Logging.Hercules](https://github.com/vostok/logging.hercules) | This library is for a log which outputs events to Hercules. |





