# Syntax

### Output Template

Represents a pattern used to render LogEvent into text representation.

There are a number of special predefined properties:

* **Timestamp** — inserts LogEvent.Timestamp formatted with given optional format. Default format is yyyy-MM-dd HH:mm:ss,fff 
* **Uptime** — inserts a current process uptime measured in milliseconds and formatted with given optional format 
* **Level** — inserts LogEvent.Level in upper case. 
* **Message** — inserts log message. 
* **NewLine** — inserts a platform-dependent newline. 
* **Exception** — inserts LogEvent.Exception with message, stack trace, inner exception and a trailing newline. 
* **Properties** — inserts all of event's LogEvent.Properties 

Ordinary named properties are referenced by their names. In the event of name collision, special predefined properties take precedence.

Examples:

```csharp
var log = new ConsoleLog(new ConsoleLogSettings
{
    OutputTemplate =
        OutputTemplate.Parse("{Timestamp:hh:mm:ss} <{Message}> {Number}{NewLine}")
});

log.WithProperty("Number", 1).Debug("Zero.");
log.WithProperty("Message", "347689").Info("One.");
log.Info("Two.");
ConsoleLog.Flush();
```

Result:

```aspnet
07:54:28 <Zero.> 1
07:54:28 <One.> 
07:54:28 <Two.> 
```

### **Message Template**

There are two kinds of properties: 

* Named properties. These should be set using logging extensions with the properties argument. 
* Positional parameters. These should be set using logging extensions with the parameters argument and are then referenced by their position in the array instead of name.

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

