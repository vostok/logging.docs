---
description: This page includes the basic concepts of Vostok.Logging
---

# Basics

### ILog

 Represents a log. 

### LogLevel

There are five log levels:

* **Debug** For verbose output. This log level should usually be ignored on production installations. ****
* **Info** For neutral messages.
* **Warn** For non-critical errors that don't interrupt the normal operation of the application.
* **Error** For unexpected errors that may require human attention.
* **Fatal** For critical errors that result in application shutdown.

```csharp
log.Debug("Verbose output");
log.Info("Neutral message");
log.Warn("Non-critical errors");
log.Error("Unexpected errors");
log.Fatal("Critical errors");
```

### LogEvent

Event consists of a timestamp, a log message, a saved exception and user-defined properties.

* **Level** _****_One of five level of the event: Debug, Info, Warn, Error, Fatal. 
* **Timestamp** The timestamp of the event. Represents the time when the event was created, rather then the time when it was written to a file or processed in any other way. 
* **Message template** The template of the log message containing placeholders to be filled with values from properties. Can be null for events containing only exception.

```csharp
log.Info("{0}.Logging!", "Vostok");
log.Info("Hello, {user}! Let's do {smth} today!", new {user="Alex", smth="nothing"});
log.Error(new Exception("Unicorn die"), "Happy Hippo");
```

* **Properties** Contains various user-defined properties of the event. There are two kinds of properties: 1. Named properties. 2.Positional parameters. 
* **Exception** The error associated with this log event.



