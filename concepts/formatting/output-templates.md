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

### Custom templates:

See the guide dedicated to custom templates usage:

{% page-ref page="../../how-to-guides/using-custom-output-templates.md" %}

### 

