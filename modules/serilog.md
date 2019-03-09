# Serilog

### Description

This library provides an intergation with [Serilog](https://serilog.net/) library in the form of an adapter that implements Vostok [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs) interface but internally relies on Serilog implementation.

### Source and packages

**GitHub repository:** [vostok/logging.serilog](https://github.com/vostok/logging.serilog)

**NuGet package**: [Vostok.Logging.Serilog](https://www.nuget.org/packages/Vostok.Logging.Serilog)

```text
Install-Package Vostok.Logging.Serilog
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```text
cm ref add vostok.logging.serilog <path-to-project>
```

### Related pages

{% page-ref page="../integrations/serilog.md" %}

