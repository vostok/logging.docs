# Basics

### ILog

 Represents a log.

### LogLevel

There are five log levels:

* **DEBUG** For verbose output. This log level should usually be ignored on production installations. ****
* **INFO**  For neutral messages.
* **WARN** For non-critical errors that don't interrupt the normal operation of the application.
* **ERROR** For unexpected errors that may require human attention.
* **FATAL** For critical errors that result in application shutdown.

```csharp
log.Debug("Verbose output");
log.Info("Neutral message");
log.Warn("Non-critical errors");
log.Error("Unexpected errors");
log.Fatal("Critical errors");
```

### LogEvent

Event consists of a timestamp, a log message, a saved exception and user-defined properties.

* _**Level**_ One of five level of the event: DEBUG, INFO, WARN, ERROR, FATAL. 
* _**Timestamp**_ The timestamp of the event. Represents the time when the event was created, rather then the time when it was written to a file or processed in any other way. 
* _**Message template**_ The template of the log message containing placeholders to be filled with values from properties. Can be null for events containing only exception.

```csharp
log.Info("{0}.Logging!", "Vostok");
log.Info("Hello, {user}! Let's do {smth} today!", new {user="Alex", smth="nothing"});
log.Error(new Exception("Unicorn die"), "Happy Hippo");
```

* _**Properties**_ Contains various user-defined properties of the event. There are two kinds of properties: 1. Named properties. These should be set using logging extensions with the 'properties' argument. 2.Positional parameters. These should be set using logging extensions with the 'parameters' argument.

```text
examples
```

* _**Exception**_ The error associated with this log event.



