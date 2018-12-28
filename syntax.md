# Syntax

### **Message Template**

smth

Examples:

```csharp
ILog log = new ConsoleLog();
            
log.Info("{0}.Logging!", "Vostok");
log.Info("\"Flowers for {hero}\" {author}", new {author="Daniel Keyes", hero="Algernon"});
log.Error(new Exception("My exception"), "Something wrong");
log.Debug("{one} two {text}", 1, "3");

ConsoleLog.Flush();
```

Result:

```aspnet
2018-11-06 13:03:40,221 INFO  Vostok.Logging!
2018-11-06 13:03:40,284 INFO  "Flowers for Algernon" Daniel Keyes
2018-11-06 13:03:40,296 ERROR Something wrong
System.Exception: My exception
2018-11-06 13:03:40,297 DEBUG 1 two 3
```

