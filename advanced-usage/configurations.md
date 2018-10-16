# Configurations

There are three ways to configure Vostok.  
Create settings file.  
Set settings provider.  
Use Vostok.Configurations.

```csharp
// configure from code — settings instance
var log1 = new FileLog(new FileLogSettings());

// configure from code — settings instance provider
var log2 = new FileLog(() => new FileLogSettings());

// configure from file
var log3 = new FileLog(new JsonFileSource("log3.json"));
```



