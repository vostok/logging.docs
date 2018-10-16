---
description: A log which outputs events to console.
---

# ConsoleLog

The implementation is asynchronous: logged messages are not immediately rendered and written to console. Instead, they are added to a queue which is processed by a background worker. 

{% hint style="info" %}
The capacity of the queue can be changed via "UpdateGlobalSettings". In case of a queue overflow some events may be dropped.
{% endhint %}

Include Logging.Console library in project:

```csharp
using Vostok.Logging.Console;
```

 An ILog is created using  `ConsoleLog`:

```csharp
var log = new ConsoleLog();
```



