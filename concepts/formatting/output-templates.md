# Output templates

[Output templates](https://github.com/vostok/logging.formatting/blob/master/Vostok.Logging.Formatting/OutputTemplate.cs) are patterns used to render [log events](../log-events.md) into text representation, shaping the output of text-based logs.

Their general syntax is identical to that of [message templates](../syntax/message-templates.md), but output templates also support a set of [special predefined properties](special-tokens.md) that do not have to be present in log events.

Ordinary properties from log events can also be included in output templates.

Output templates can also contain uninterpreted text.

### Default template

Default output template looks like this:

```text
{Timestamp} {Level} {TraceContext:w}{OperationContext:w}{SourceContext:w}{Message}{NewLine}{Exception}
```

See the list of [special properties](special-tokens.md) to understand the bulk of this template's content. 

See the sections about [source context](../source-context.md) and [operation context](../operation-context.md) to learn more about corresponding well-known properties mentioned in this template. 

See [format specifiers](format-specifiers.md) section to find out how the `:w` modifier works. 

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

