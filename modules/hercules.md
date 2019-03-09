# Hercules

### Description

This library contains an [implementation](../implementations/file-log.md) of ILog that sends events to [Hercules](https://github.com/vostok/hercules) using provided [IHerculesSink](https://github.com/vostok/hercules.client.abstractions/blob/master/Vostok.Hercules.Client.Abstractions/IHerculesSink.cs) implementation. It also provides mapping from Hercules events back to log events model.

### Source and packages

**GitHub repository:** [vostok/logging.hercules](https://github.com/vostok/logging.hercules)

**NuGet package**: [Vostok.Logging.Hercules](https://www.nuget.org/packages/Vostok.Logging.Hercules)

```text
Install-Package Vostok.Logging.Hercules
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```text
cm ref add vostok.logging.hercules <path-to-project>
```

### Related pages

{% page-ref page="../implementations/hercules-log.md" %}

