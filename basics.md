---
description: This page includes the basic concepts of Vostok.Logging
---

# Basics

### [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs)

The main interface, represents a log.   
There are two [standard log implementations](implementations/) in Vostok, developers use `ILog` to write their own implementations.

`ILog` has three methods:

| Method | Description |
| :--- | :--- |
| Log | Logs the given `LogEvent`. Read more about extensions [here](syntax.md#log-extensions). |
| IsEnabledFor | Returns whether the current log is configured to log events of the given `LogLevel`. |
| ForContext | Returns a copy of the log operating in the given source context. For details, see [Advanced usage](advanced-usage/custom-implementations.md#for-context). |

### [LogEvent](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/LogEvent.cs)

Event consists of a level, a timestamp, a log message, a saved exception and user-defined properties.

\*\*\*\*[**Level**](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/LogLevel.cs)  
****One of five level of the event:

* **Debug** For verbose output.
* **Info** For neutral messages.
* **Warn** For non-critical errors that don't interrupt the normal operation of the application.
* **Error** For unexpected errors that may require human attention.
* **Fatal** For critical errors that result in application shutdown.

**Timestamp**  
Represents the time when the event was created.

**Message template**  
The template of the log message containing placeholders to be filled with values from.  
A few examples can be found [here](syntax.md#message-template).

**Properties**  
Contains various user-defined properties of the event.

**Exception**  
The error associated with this log event.

{% hint style="info" %}
You don't need to create LogEvent yourself, extensions do it for you.

Learn more about how to use extension syntax [here](syntax.md).
{% endhint %}





