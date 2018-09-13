# ConsoleLog

A log which outputs events to console.  
The implementation is asynchronous: logged messages are not immediately rendered and written to console. Instead, they are added to a queue which is processed by a background worker. 

{% hint style="info" %}
The capacity of the queue can be changed via "UpdateGlobalSettings". In case of a queue overflow some events may be dropped.
{% endhint %}

some text

```csharp
using Vostok.Logging.Console;
```

smth

```csharp
var log = new ConsoleLog();
```

smth



