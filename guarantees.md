---
description: Guarantees of implementations of logs out of the box.
---

# Guarantees

### Errors

If the log events cannot be written for any reason \(such as running out of disk space\), the library will not throw an exception. Instead, the process will repeat later in the background.

### Async input/output

If log events can't be written for any reason, we put them in a buffer and handle them later.

### **Bounded memory usage**

Implementations are limited in the amount of memory they occupy. The buffer size is customizable.

### Log events can be lost!

If the application crashes or it can't send logs for a long time, log events will be lost.   
We guarantee that one of these fine days this will happen and you lose your logs.  
And we don't recommend building business processes that depend on log events.  
  
  
****

