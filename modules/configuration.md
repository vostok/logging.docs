# Configuration

### Description

This library contains [ConfigurableLog](https://github.com/vostok/logging.configuration/blob/master/Vostok.Logging.Configuration/ConfigurableLog.cs) — an implementation of `ILog` that aggregates multiple named loggers and allows to dynamically configure filtering and enrichment rules from external sources.

### Source and packages

**GitHub repository:** [vostok/logging.configuration](https://github.com/vostok/logging.configuration)

**NuGet package**: [Vostok.Logging.Configuration](https://www.nuget.org/packages/Vostok.Logging.Configuration/)

```text
Install-Package Vostok.Logging.Configuration
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```text
cm ref add vostok.logging.configuration <path-to-project>
```

### Related pages

{% page-ref page="../how-to-guides/external-configuration-rules.md" %}

