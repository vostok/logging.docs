# Microsoft

### Description

This library provides an implementation of ILoggerProvider from [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/) built on top of user-provided Vostok [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs) instance. It enables the use of Vostok logging in ASP.NET Core web applications.

### Source and packages

**GitHub repository:** [vostok/logging.microsoft](https://github.com/vostok/logging.microsoft)

**NuGet package**: [Vostok.Logging.Microsoft](https://www.nuget.org/packages/Vostok.Logging.Microsoft)

```text
Install-Package Vostok.Logging.Microsoft
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```text
cm ref add vostok.logging.microsoft <path-to-project>
```

### Related pages

{% page-ref page="../integrations/microsoft-logging.md" %}

