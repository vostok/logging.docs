# Guarantees

This page lists the guarantees provided by built-in log implementations \([console log](implementations/console-log.md), [file log](implementations/file-log.md) and [Hercules log](implementations/hercules-log.md)\). These guarantees reflect the following design principle: logging system should not be able to affect overall application health and performance. 

#### No exceptions from logging methods

If log events cannot be saved for any reason \(ranging from incorrect [message template](concepts/syntax/message-templates.md) to running out of disk space or experiencing remote backend unavailability\), log methods still complete successfully without throwing exceptions. If possible, a diagnostic message is produced via secondary means \(console output for [file log](implementations/file-log.md) and any local log for [Hercules log](implementations/hercules-log.md)\).

#### Asynchronous I/O

Log methods always return instantly \(and are mostly lock-free\). All the necessary I/O \(writing to file/console or sending HTTP requests\) happens in the background.

#### Limited resource usage

Async I/O implies buffering. Log implementations have configurable limits on internal buffer sizes to avoid allocating too much memory. CPU usage is generally bounded to a single core.

#### No guaranteed delivery

Logs delivery is maintained on a best effort basis. Logs in Vostok are treated as a diagnostic tool as opposed to a business process building block.

Events can be lost in following cases:

* Internal buffers overflow due to unavailability of underlying storage or sheer volume of incoming logs.
* Application terminates abruptly without flushing/disposing async loggers.

 

