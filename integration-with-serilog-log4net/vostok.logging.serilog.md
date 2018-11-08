---
description: Represents an adapter between Vostok logging interfaces and Serilog.
---

# Vostok.Logging.Serilog

Если вы уже пользуетесь Serilog, но хотите попробовать Восточную реализацию, есть специальная библиотека [Vostok.Logging.Serilog](https://github.com/vostok/logging.serilog). С её помощью не придётся переписывать всё логирование. Создаете адаптер и получаете восточный фасад у имеющегося лога.

### First usage

Create an Serilog `ILogger`:

```csharp
var log = new LoggerConfiguration()
    .WriteTo.Console()
    .CreateLogger();
```

Create an adapter с которым будем работать дальше:

```csharp
ILog adapter = new SerilogLog(log);
```

Let's try to work with it as with Vostok's ILog. Выведем какое-нибудь информационное сообщение:

```csharp
adapter.Info("Easy Vostok");
```

Заметим, что хоть мы и обращались с логом как с восточным, на консоль вывелся формат Serilog'а:

```aspnet
[13:36:38 INF] Easy Vostok
```

Почему так произошло?  
У нас был лог Serilog, мы построили адаптер, чтобы обращаться к этому логу как к восточному, но внутри всё осталось прежним.

### Example 1

Попробуем сделать что-нибудь чуть более сложное.  
Для начала создадим простой восточный файловый лог:

```csharp
var fileLog = new FileLog(new FileLogSettings
{
    FilePath = "log.log"
});
```

Сейчас мы хотим построить такой лог, чтобы мы могли одновременно писать информацию в консоль и в файл.  
У нас есть лог Serilog, который пишет в консоль, и восточный лог, который пишет в файл.  
Не хватает только единого входа, чтобы логи писались одновремннно.  
Для этого построим композитный лог и передадим ему fileLog и adapter.  
Мы работаем с адаптером, потому что композитный лог принимает только восточные реализации.

```csharp
var composite = new CompositeLog(fileLog, adapter);

composite.Error("something wrong");

fileLog.Flush();
```

В результате в консоли мы увидим информацию в формате Serilog, а в файле формат будет восточным:

```aspnet
Console:
[14:10:22 INF] Easy Vostok
[13:36:39 ERR] Something wrong

File:
2018-11-08 13:36:39,119 ERROR Something wrong
```

### Example 2

Ещё немного усложним предыдущий код и посмотрим что произойдет.  
Создадим ивент с добавленными свойствами, передадим его в созданный `composite`:

```csharp
 var event2 = new LogEvent(LogLevel.Info, DateTimeOffset.Now, "Show me text")    
    .WithProperty("Priority", 2)    
    .WithProperty("Author", "Service127");
 
composite.Log(event2);
```

Дополнительно настроим файловый лог, чтобы мы видели добавленные свойства:

```csharp
var fileLog = new FileLog(new FileLogSettings
{
    FilePath = "log.log",
    OutputTemplate = OutputTemplate.Parse("{TimeStamp:hh:mm:ss} {Message} {Priority} {Author} {Exception}{NewLine}")
});
```

В результате в консоли мы получим следующий вывод:

```aspnet
Console:
[14:10:22 INF] Easy Vostok
[14:10:22 ERR] Something wrong
[14:10:22 INF] Show me text

File:
02:10:22 Something wrong   
02:10:22 Show me text 2 Service127 
```

Настройки, которые были у начального лога Serilog сохранились, свойства не обработались.  
Из-за того что мы изменили настройки  `fileLog` , в файле оказалась вся информация, переданная с логом, включая свойства.

