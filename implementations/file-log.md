# File log

**Location**: [file module](../modules/file.md).

```csharp
var fileLog = new FileLog(new FileLogSettings());
```



### Features

* Customizable [output templates](../concepts/formatting/output-templates.md).
* Customizable rolling strategies:
  * By size
  * By time
  * Hybrid
  * Automatic cleanup of stale files
* `Log` method is nonblocking: log events are placed into an internal queue, grouped into batches and efficiently written to files in the background.
* Multiplexing: multiple `FileLog` instances inside a single process may write to the same file without performance penalties.



TODO

