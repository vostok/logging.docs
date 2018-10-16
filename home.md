# Home

## Libraries

#### Logging.Abstractions

This library is a facade with core logging interfaces and models \([ILog](untitled.md#ilog), [LogEvent](untitled.md#logevent), [LogLevel](untitled.md#loglevel)\) and a set of useful extensions.

#### Logging.Console

This library is for a log which outputs events to console. Supports color-marked messages, uses lock-free queue for asynchronous message writing.

#### Logging.File

This library is for a log which outputs events to file. Supports rolling-strategies for logs rotation, uses lock-free queue for asynchronous message writing, easy to configure from code and other sources.

#### Logging.Context

Automatically adds info to log messages from background context \(ссылка на доку, которой ещё нет\)

#### Logging.Formatting

Rendering messages and events to document. Can be used in your realisations of text logging.

#### [Logging.Log4Net](integration-with-serilog-log4net/)

Represents an adapter between Vostok logging interfaces and log4net.

#### [Logging.Serilog](integration-with-serilog-log4net/)

Represents an adapter between Vostok logging interfaces and Serilog.

#### Logging.Hercules





