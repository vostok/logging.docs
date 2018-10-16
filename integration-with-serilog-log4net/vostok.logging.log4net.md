---
description: Represents an adapter between Vostok logging interfaces and log4net.
---

# Vostok.Logging.Log4Net

It implements Vostok ILog interface using an externally provided instance of log4net ILogger.  
It does this by following these rules:

* LogLevels are directly translated to log4net Level;
* Messages are prerendered into text as Vostok ILog's formatting syntax differs from log4net;
* Properties are forwarded into log4net event's LoggingEvent.Properties;
* ForContext with null argument returns a Log4netLog based on root logger from log4net's repository;
* ForContext with non-null argument returns a Log4netLog based on logger with name equal to context value, obtained with ILoggerRepository.GetLogger;

### Example

Допустим, используется Log4Net. 

```csharp
public static class Logger
    {
        private static ILog log = LogManager.GetLogger("LOGGER");


        public static ILog Log
        {
            get { return log; }
        }

        public static void InitLogger()
        {
            XmlConfigurator.Configure();
        }
    }
```

```csharp
Logger.InitLogger();
```

Create an adapter:

```csharp
adapter = new Log4netLog(log4netLogger);
```

Let's try to work with it as with Vostok's ILog:

```text

```

