# Custom output templates

**Prerequisites**: install [formatting](../concepts/formatting/) module, use one of text-based logs \([console](../implementations/console-log.md) or [file](../implementations/file-log.md)\).

### Constructing custom templates

There are two ways to obtain a custom template:

* Parse it from an arbitrary string:
  * ```csharp
    var template = OutputTemplate.Parse("Here's the message: {Message}{NewLine}");
    ```
* Use `OutputTemplateBuilder` to construct it in code: 
  * ```csharp
    var template = new OutputTemplateBuilder()
        .AddText("Here's the message: ")
        .AddMessage()
        .AddNewline()
        .Build();
    ```

### Passing to a log instance

Custom output templates can be passed to text-based logs as parameters in their respective settings:

```csharp
var log = new ConsoleLog(new ConsoleLogSettings
{
    OutputTemplate = customTemplate
});
```

```csharp
var log = new FileLog(new FileLogSettings
{
    OutputTemplate = customTemplate
});
```

