# Syntax

### Log Extensions

The `Log`  method uses one of the following extension methods:

* Logs the given message on the _X_ level without any additional properties. 
* Logs the given exception on the _X_ level without a message or any additional properties. 
* Logs the given message and exception on the _X_ level without any additional properties. 
* Logs the given messageTemplate on the _X_ level with given properties. The messageTemplate can contain placeholders for properties. 
* Logs the given messageTemplate on the _X_ level with given parameters. The messageTemplate can contain placeholders for parameters. 
* Logs the given messageTemplate and exception on the _X_ level with given properties. The messageTemplate can contain placeholders for properties. 
* Logs the given messageTemplate and exception on the _X_ level with given parameters. The messageTemplate can contain placeholders for parameters.

_X_ – one of five log levels: Info, Debug, Warn, Error, Fatal.

### Template syntax

The template "foo{0} {key}" and properties { '0': 'bar', 'key': 'baz' } produce the following output: "foobar baz".  
Use double curly braces to escape curly braces in text: "{{key}}", new {key = "value"} --&gt; "{key}".  
Any mismatched braces or nonexistent keys are kept as-is: "key1} {key2}", { 'key1': 'value' } --&gt; "key1} {key2}".

### Message Template

The template of the log message containing placeholders to be filled with values from Properties. Can be null for events containing only Exception.  
There are two kinds of properties: 

* Named properties. These should be set using logging extensions with the properties argument. 
* Positional parameters. These should be set using logging extensions with the parameters argument and are then referenced by their position in the array instead of name.

If the template uses named parameters, the values will be substituted only for those for which they exist. Otherwise, the parameters are substituted in the order in which they are written.

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

### Output Template

Output Template represents a pattern used to render LogEvent into text representation.

There are a number of special predefined properties:

* **Timestamp** — inserts LogEvent.Timestamp formatted with given optional format. Default format is yyyy-MM-dd HH:mm:ss,fff 
* **Uptime** — inserts a current process uptime measured in milliseconds and formatted with given optional format 
* **Level** — inserts LogEvent.Level in upper case. 
* **Message** — inserts log message. 
* **NewLine** — inserts a platform-dependent newline. 
* **Exception** — inserts LogEvent.Exception with message, stack trace, inner exception and a trailing newline. 
* **Properties** — inserts all of event's LogEvent.Properties Ordinary named properties are referenced by their names. In the event of name collision, special predefined properties take precedence.

There are two built-in output template:

* `OutputTemplate.Dafault` – A default template with following representation:  "{Timestamp} {Level} {Prefix}{Message}{NewLine}{Exception}". 
* `OutputTemplate.Empty` – A template that always produces empty text regardless of LogEvent contents.

You can customize output format using the `OutputTemplate` in the `LogSettings`.  Add the parameters you want to see in the final message to the template. Other parameters will be ignored.  
If there is a parameter in the template, but this parameter is not in the event, a message without this parameter will be displayed.

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

