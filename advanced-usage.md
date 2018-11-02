# Advanced usage

## //

## 

## 

## 

## 

## 

## 

## UseCases

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
var log1 = new FileLog( new FileLogSettings
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

### Selective logging

```csharp
var log = new FileLog( new FileLogSettings
{
    FilePath = "log.txt",
    EnabledLogLevels = new[] {
    LogLevel.Warn, LogLevel.Error },
});
FileLog.FlushAll();
```

### Synchronous logging to file and console

```csharp
ILog log1 = new FileLog(
    new FileLogSettings
    {
        FilePath = "l.log"
    });
            
ILog log2 = new ConsoleLog();
            
CompositeLog composite = new CompositeLog(log1, log2);
            
composite.Info("test");
            
ConsoleLog.Flush();
FileLog.FlushAll();
```

### Rolling Strategy

```csharp
var log = new FileLog(new FileLogSettings
{
    FilePath = "log.txt",
    RollingStrategy = new FileLogSettings.RollingStrategyOptions
    {
        MaxFiles = 3,
        MaxSize = 50.Megabytes(),
        Period = 2.Days(),
        Type = RollingStrategyType.Hybrid
    }
});
```

### Color-marked console messages 

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





