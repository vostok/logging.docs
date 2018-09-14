# Integration with SeriLog/Log4Net

bla-bla-bla  
A bridge from Vostok to Serilog/Log4Net .  
bla-bla-bla

### Vostok.Logging.Serilog

Represents an adapter between Vostok logging interfaces and Serilog.  
It implements Vostok ILog interface using an externally provided instance of Serilog ILogger.   
It does this by following these rules:

* Vostok LogLevel are directly translated to Serilog SerilogLevel;
* Messages are not prerendered into text as Vostok ILog's formatting syntax capabilities are a subset of those supported by Serilog;
* Message templates are parsed using ILogger.BindMessageTemplate;
* Event properties are converted using ILogger.BindProperty;
* ForContext invokes inner ILogger's ILogger.ForContext\(string,object,bool\) with name set to Constants.SourceContextPropertyNameand wraps resulting ILogger into another SerilogLog.

```csharp
example
```

### Vostok.Logging.Log4Net

Represents an adapter between Vostok logging interfaces and log4net.  
It implements Vostok ILog interface using an externally provided instance of log4net ILogger.  
It does this by following these rules:

* LogLevels are directly translated to log4net Level;
* Messages are prerendered into text as Vostok ILog's formatting syntax differs from log4net;
* Properties are forwarded into log4net event's LoggingEvent.Properties;
* ForContext with null argument returns a Log4netLog based on root logger from log4net's repository;
* ForContext with non-null argument returns a Log4netLog based on logger with name equal to context value, obtained with ILoggerRepository.GetLogger;

```text
example
```



