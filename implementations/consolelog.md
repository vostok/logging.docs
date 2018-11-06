---
description: A log which outputs events to console.
---

# ConsoleLog

### SetUp

Для работы с логом, выводящим информацию на консоль  
Include `Logging.Console` library in project:

```csharp
using Vostok.Logging.Console;
```

 An standard `ILog` is created using  `ConsoleLog`:

```csharp
var log = new ConsoleLog();
```

Теперь можем создать различные события.  
Пусть это будет сообщение об ошибке

```csharp
log.Error("Error number 1");
```

Делать так можно сколько угодно раз:

```csharp
for (int i = 1; i <= 100; i++)
{
    log.Error("Error number {0}",i);
}
```

Чтобы увидеть результат, необходимо использовать `ConsoleLog.Flush()` или `ConsoleLog.FlushAsync()`. 

Result:

```aspnet
2018-11-06 17:36:04,702 ERROR Error number 1
...
2018-11-06 17:36:04,789 ERROR Error number 100
```

### First Usage

Теперь попробуем настроить наш лог с помощью `ConsoleLogSettings` .   
Например, изменим формат вывода логов. Будем выводить только время и текст сообщения. Весь остальной код оставим прежним:

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

Конфигурация консольного лога происходит в коде. Как мы это проделали в примере выше. 

### Settings

* \*\*\*\*[**OutputTemplate**](https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs)
* [**FormatProvider**](https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs)
* [**ColorMapping**](https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs)
* [**ColorsEnabled**](https://github.com/vostok/logging.console/blob/master/Vostok.Logging.Console/ConsoleLogSettings.cs)\*\*\*\*



