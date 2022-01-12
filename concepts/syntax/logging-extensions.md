# Logging extensions

[Abstractions module](../../modules/abstractions.md) provides a wide set of extensions that take care of constructing [log events](../log-events.md).

These extensions can be grouped in two ways:

*   By level and name: **Debug**, **Info**, **Warn**, **Error**, **Fatal**.


* By parameters:
  *   **string**:

      * Produces an event with given [message template](message-templates.md) and no properties.
      * ```csharp
        log.Info("Hello, world!");
        ```


  *   **string + T**:

      * Produces an event with given [message template](message-templates.md) and properties of given object.
      * ```csharp
        log.Info("Hello, {Who}!", new { Who = "world" });
        ```


  *   **string + object\[]**:

      * Produces an event with given [message template](message-templates.md) and given property values (names are inferred from message template).
      * ```csharp
        log.Info("Hello, {Who}!", "world");
        ```


  *   **Exception**:

      * Produces an event with given exception and no message or properties.
      * ```csharp
        log.Error(new Exception());
        ```


  *   **Exception + string**:

      * Produces an event with given exception and [message template](message-templates.md).
      * ```csharp
        log.Error(new Exception(), "I have failed.");
        ```


  *   **Exception + string + T**:

      * Produces an event with given exception, [message template](message-templates.md) and properties of given object.
      * ```csharp
        log.Error(new Exception(), "{Who} have/has failed.", new { Who = "I" });
        ```


  *   **Exception + string + object\[]**:

      * Produces an event with given exception, [message template](message-templates.md) and given property values (names are inferred from message template).
      * ```csharp
        log.Error(new Exception(), "{Who} have/has failed.", "He");
        ```


  * **interpolated string**:
    * Produces an event with given [message template](message-templates.md) and given property values (names are extracted from argument names).
    * [Requires](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-10.0/improved-interpolated-strings) C# 10.
    * ```csharp
      var Who = "world";
      log.Info($"Hello, {Who}!");
      ```
  * **Exception + interpolated string**:
    * Produces an event with given exception, [message template](message-templates.md) and given property values (names are extracted from argument names).
    * [Requires](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-10.0/improved-interpolated-strings) C# 10.
    * ```csharp
      var Who = "world";
      log.Info(new Exception(), $"Hello, {Who}!");
      ```



See the section about [providing property values](passing-properties.md) to extensions to get a grasp of how to provide values for placeholders in message template.

All extensions produce events with timestamp set to current time and level corresponding to method name.
