# Abstractions

### Description

This library contains core interfaces and models, such as [ILog](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/ILog.cs) and [LogEvent](https://github.com/vostok/logging.abstractions/blob/master/Vostok.Logging.Abstractions/LogEvent.cs). It also hosts a wide set of [extensions](https://github.com/vostok/logging.abstractions/tree/master/Vostok.Logging.Abstractions/Extensions) implemented through ILog decorators.

### Source and packages

**GitHub repository:** [vostok/logging.abstractions](https://github.com/vostok/logging.abstractions)

**NuGet package**: [Vostok.Logging.Abstractions](https://www.nuget.org/packages/Vostok.Logging.Abstractions/)

```text
Install-Package Vostok.Logging.Abstractions
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```text
cm ref add vostok.logging.abstractions <path-to-project>
```

### Related pages

{% page-ref page="../concepts/log-events.md" %}

{% page-ref page="../concepts/log-interface.md" %}

{% page-ref page="../concepts/syntax/" %}

{% page-ref page="../concepts/source-context.md" %}

{% page-ref page="../use-cases/combining-multiple-logs.md" %}

{% page-ref page="../use-cases/filtering-events-by-level.md" %}

{% page-ref page="../use-cases/filtering-events-by-properties.md" %}

{% page-ref page="../use-cases/enriching-events-with-custom-properties.md" %}

{% page-ref page="../use-cases/using-static-log-provider.md" %}

