---
description: A log which outputs events to a file.
---

# FileLog

The implementation is asynchronous and thread-safe: logged messages are not immediately rendered and written to file. Instead, they are added to a lock-free queue which is processed by a background worker.

{% hint style="info" %}
The capacity of the queue can be changed in settings if a settings provider is used. In case of a queue overflow some events may be dropped. 
{% endhint %}

Use `Flush` or `FlushAsync` to ensure that logged events are written to file.  
Use `EventsLost` counter to see how many events were lost due to queue overflow.  
Remember to Dispose a FileLog instance when you no longer need it to close the file handle.  
Log method never throws exceptions. On the other hand, `Flush` and `FlushAsync` may do so.

Include `Logging.File` library in project:

```csharp
using Vostok.Logging.File;
```

 An `ILog` is created using `FileLog`:

```csharp
var log = new FileLog(
    new FileLogSettings { FilePath = "log.txt" });
```



