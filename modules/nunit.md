# NUnit

### Description

This library provides an implementation of ILog that can be used in NUnit tests.

An instance of NUnitLog can log into different contexts of tests depending on the requirements.

### Source and packages

**GitHub repository:** [vostok/logging.nunit](https://github.com/vostok/logging.nunit)

**NuGet package**: [Vostok.Logging.NUnit](https://www.nuget.org/packages/Vostok.Logging.NUnit)

```
Install-Package Vostok.Logging.NUnit
```

[Cement](https://github.com/skbkontur/cement) users should reference this module with the following command:

```
cm ref add vostok.logging.nunit <path-to-project>
```

### Details

#### Current test context

```csharp
var settings = NUnitLogSettings.WithCurrentTestContext();
var log = new NUnitLog(settings);
```

This type of context writes log events to the context of the test in which the log was created.

#### AsyncLocal context

```csharp
var settings = NUnitLogSettings.WithAsyncLocalContext();
var log = new NUnitLog(settings);
```

This type of context writes log events to the context which is retrieved from AsyncLocal static variable. It usually contains context of the current test, but in some cases (which involve launching something on a different thread, like a service, for instance) may write to the unknown context, therefore leading to losing logs.

It is recommended to create log instances using **Current test context** in such cases.

