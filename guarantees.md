---
description: The library does not affect the operation of the application.
---

# Guarantees

### Errors

An app does not get exceptions.  
Library level errors do not reach an application level. \(Errors will be taken into account on library level\)  
If we can't write a log for any reason, the library will not throw an exception. Instead, repeat the process in the background after a while.

### Async input/output

If we can't write a log for any reason, we put them in a buffer and deal with them later.

### **Bounded memory usage**

Internal buffers can't eat all memory.  
Implementations are limited in the amount of memory they occupy. The buffer size is customizable.

### Log events can be lost!

If the application crashes, it can't send logs for a long time, log events will be lost.   
We guarantee that someday this will happen and you lose your logs.  
  
  
****

