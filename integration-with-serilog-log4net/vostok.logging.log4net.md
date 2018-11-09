---
description: Represents an adapter between Vostok logging interfaces and log4net.
---

# Vostok.Logging.Log4net

Если вы уже пользуетесь Log4net, но хотите попробовать Восточную реализацию, есть специальная библиотека Vostok.Logging.Log4net. С её помощью не придётся переписывать всё логирование. Создаете адаптер и получаете восточный фасад у имеющегося лога.

### First usage

Create an Log4net `ILog`:

```csharp
private static readonly log4net.ILog log = LogManager.GetLogger
            (System.Reflection.MethodBase.GetCurrentMethod().DeclaringType);

static void Main(string[] args)
{
    var logRepository = LogManager.GetRepository(Assembly.GetEntryAssembly());
    XmlConfigurator.Configure(logRepository, new FileInfo("log4net.config"));
}
```

Create an adapter с которым будем работать дальше:

```csharp
 var adapter = new Log4netLog(log);
```

Let's try to work with it as with Vostok's ILog. Выведем какое-нибудь информационное сообщение:

```csharp
adapter.Info("test");
```

Заметим, что хоть мы и обращались с логом как с восточным, на консоль вывелся формат Log4net'а:

```aspnet
2018-11-09 11:59:06,776 INFO Log.Program - test
```

Почему так произошло?  
У нас был лог Log4net, мы построили адаптер, чтобы обращаться к этому логу как к восточному, но внутри всё осталось прежним.

### Example 1

Попробуем сделать что-нибудь чуть более сложное.  
Для начала создадим простой восточный файловый лог:

```csharp
var fileLog = new FileLog(new FileLogSettings
{
    FilePath = "log.log"
});
```

Сейчас мы хотим построить такой лог, который позволит одновременно писать информацию в консоль и в файл.  
У нас есть лог Log4net, который пишет в консоль, и восточный лог, который пишет в файл.  
Не хватает только единого входа, чтобы логи писались одновремннно.  
Для этого построим композитный лог и передадим ему fileLog и adapter.  
Мы работаем с адаптером, потому что композитный лог принимает только восточные реализации.

```csharp
var composite = new CompositeLog(fileLog, adapter);

composite.Error("something wrong");

fileLog.Flush();
```

В результате в консоли мы увидим информацию в формате Log4net, а в файле формат будет восточным:

```aspnet
Console:
2018-11-09 12:02:34,209 INFO Log.Program - test
2018-11-09 12:02:34,304 ERROR Log.Program - something wrong

File:
2018-11-09 12:02:34,304 ERROR something wrong
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
2018-11-09 12:03:35,169 INFO Log.Program - test
2018-11-09 12:03:35,288 ERROR Log.Program - something wrong
2018-11-09 12:03:35,280 INFO Log.Program - Show me text

File:
12:03:35 something wrong   
12:03:35 Show me text 2 Service127 
```

Настройки, которые были у начального лога Log4net сохранились, свойства не обработались.  
Из-за того что мы изменили настройки  `fileLog` , в файле оказалась вся информация, переданная с логом, включая свойства.

