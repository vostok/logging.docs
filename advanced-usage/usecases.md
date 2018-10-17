---
description: Examples of using and individual settings
---

# UseCases

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

### Synchronous logging to several files

### Synchronous logging to file and console

### Configuring color-marked console messages 

```csharp
var log = new ConsoleLog(new ConsoleLogSettings
{
    ColorMapping = new Dictionary<LogLevel, ConsoleColor>
    {
        {LogLevel.Debug, ConsoleColor.Red},
        {LogLevel.Info, ConsoleColor.Cyan},
        {LogLevel.Warn, ConsoleColor.DarkYellow},
        {LogLevel.Error, ConsoleColor.Green},
        {LogLevel.Fatal, ConsoleColor.Magenta},
    }
});
    
log.Debug("Red");
log.Info("Cyan");
log.Warn("DarkYellow");
log.Error("Green");
log.Fatal("Magenta");
ConsoleLog.Flush();
```



