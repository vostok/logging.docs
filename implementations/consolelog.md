---
description: A log which outputs events to console.
---

# ConsoleLog

### SetUp

Include `Logging.Console` library in project:

```csharp
using Vostok.Logging.Console;
```

 An standard `ILog` is created using  `ConsoleLog`:

```csharp
var log = new ConsoleLog();
```

Now you can create different events. Let it be error message:

```csharp
log.Error("Error number 1");
```

You can add as many events as you want: 

```csharp
for (int i = 1; i <= 100; i++)
{
    log.Error("Error number {0}",i);
}
```

To observe the result, add `ConsoleLog.Flush()` or `ConsoleLog.FlushAsync()`. 

Result:

```aspnet
2018-11-06 17:36:04,702 ERROR Error number 1
...
2018-11-06 17:36:04,789 ERROR Error number 100
```

### First Usage

Let's try to configure a log and use `ConsoleLogSettings` for it.   
For example, you can change output template. The log would show only time stamp and message. We'll leave the rest of the code the same:

```csharp
var consoleLog = new ConsoleLog(new ConsoleLogSettings
{
    OutputTemplate = OutputTemplate.Parse("{TimeStamp:hh:mm:ss} {Message}{NewLine}")
});

for (int i = 1; i <= 100; i++)
{
    consoleLog.Error("Error number {0}",i);
}

ConsoleLog.Flush();
```

Result:

```text
06:06:51 Error number 1
...
06:06:51 Error number 100
```

### Configurations 

Console log's configuration passes in code \(the example above\). 

### Settings

This parameters are adjusted in `ConsoleLogSettings`:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameters</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs"><b>OutputTemplate</b></a>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>used to render log messages</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs"><b>FormatProvider</b></a>
        </p>
      </td>
      <td style="text-align:left">
        <br />If specified, this IFormatProvider will be used when formatting log events.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs"><b>ColorMapping</b></a>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>Mapping of log levels to text color in console</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs"><b>ColorsEnabled</b></a><b></b>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>Specifies whether the console log must colorize text depending on the
          log level</p>
      </td>
    </tr>
  </tbody>
</table>



