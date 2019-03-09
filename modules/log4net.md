# Log4net

### Description

This library provides an intergation with [log4net](https://logging.apache.org/log4net/) library in the form of an adapter that implements Vostok [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs) interface but internally relies on log4net implementation.

### Source and packages

**GitHub repository:** [vostok/logging.log4net](https://github.com/vostok/logging.log4net)

**NuGet package**: [Vostok.Logging.Log4net](https://www.nuget.org/packages/Vostok.Logging.Log4net)

```text
Install-Package Vostok.Logging.Log4net
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```text
cm ref add vostok.logging.log4net <path-to-project>
```

### Related pages

{% page-ref page="../integrations/log4net.md" %}

