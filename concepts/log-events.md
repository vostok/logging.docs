# Log events

[Log event](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/LogEvent.cs) is the atomic unit of logging data: every act of logging produces one.

{% hint style="info" %}
Users are typically not required to create log events manually as numerous [logging extensions](syntax/logging-extensions.md) handle event construction, unless they are building a custom log implementation/decorator.
{% endhint %}

### Structure

Every log event consists of five components:

* **Level**

  * Levels indicate event severity:
    * **Debug**: verbose output, typically disabled in production
    * **Info:** neutral messages
    * **Warn:** non-critical errors that don't affect the normal operation of the application
    * **Error:** unexpected errors that may require human attention
    * **Fatal:** critical errors resulting in application shutdown

* **Timestamp**

  * Timestamp of the event creation. Includes timezone information.

* **Message template**

  * [Template](syntax/message-templates.md) of the log message that may contain placeholders to be filled with values from properties. May be absent in a valid log event.

* **Properties**

  * Arbitrary key-value data with case-sensitive string keys. May be absent in a valid log event.

* **Exception**

  * The error associated with the log event. May be absent in a valid log event.

### Immutability

Log events are effectively immutable: any changes lead to creation of a new event. `LogEvent` class provides a set of special transformation methods:

```csharp
logEvent = logEvent.WithProperty("Count", 100);
logEvent = logEvent.WithoutProperty("UselessProperty");
```

This ensures thread safety when routing the same event to multiple logs.

