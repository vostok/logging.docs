---
description: The library does not affect the operation of the application.
---

# Guarantees

### Errors

An app doesn't get exceptions.  
Library level errors do not reach an application level. Errors will be taken into account on library level. If log events can't be written for any reason \(for example, a file is closed\), the library will not throw an exception. Instead, the process will repeat later in the background.

### Async input/output

If log events can't be written for any reason, we put them in a buffer and deal with them later.

### **Bounded memory usage**

Internal buffers can't eat all memory.  
Implementations are limited in the amount of memory they occupy. The buffer size is customizable.

### Log events can be lost!

If the application crashes, it can't send logs for a long time, log events will be lost.   
We guarantee that one of these fine days this will happen and you lose your logs.  
And we don't recommend building business processes that depend on log events.  
  
  
****

