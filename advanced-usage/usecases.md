# UseCases

### Configuring color-marked console messages 

```csharp
var log = new ConsoleLog(new ConsoleLogSettings
{
    ColorMapping = new Dictionary<LogLevel, ConsoleColor>
    {
        {LogLevel.Debug, (ConsoleColor)random.Next(16)},
        {LogLevel.Info, (ConsoleColor)random.Next(16)},
        {LogLevel.Warn, (ConsoleColor)random.Next(16)},
        {LogLevel.Error, (ConsoleColor)random.Next(16)},
        {LogLevel.Fatal, (ConsoleColor)random.Next(16)},
    }
});

log.Debug("1");
log.Info("2");
log.Warn("3");
log.Error("4");
log.Fatal("5");
ConsoleLog.Flush();
```

### Adding context prefixes

```csharp
ILog log = new ConsoleLog(new ConsoleLogSettings
    {
        ColorsEnabled = true,
        OutputTemplate = OutputTemplate.Default
    });
                  
      log = log.WithContextualPrefix();
       
      using (new ContextualLogPrefix("op-1"))
          {
              log.Info("Message 1!");
                      
              using (new ContextualLogPrefix("op-2"))
              {
                  log.Info("Message 2!");
              }
                      
              log.Info("Message 3!");
          }
  ConsoleLog.Flush();
```

### Synchronous logging to several files

### Synchronous logging to file and console

### Selected logging

```csharp
var log = new FileLog(new FileLogSettings
{
    FilePath = "log.txt",
    EnabledLogLevels = new[] {
    LogLevel.Warn, LogLevel.Error },
});
FileLog.FlushAll();
```

### Messages output format configuration

```csharp
var log1 = new FileLog(new FileLogSettings
{
    FilePath = "log.txt",
    OutputTemplate = OutputTemplate.Default
});

var log2 = new FileLog(new FileLogSettings
{
    FilePath = "log.txt",
    OutputTemplate =
        OutputTemplate.Parse("{Timestamp:hh:mm:ss} <{Message}>{NewLine}")
});

log1.Info("One."); log2.Info("Two."); log1.Info("Three."); log2.Info("Four.");
FileLog.FlushAll();
```



