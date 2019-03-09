# Providing property values

There are three supported ways to pass property values for placeholders in [message template](message-templates.md) when using [logging extensions](logging-extensions.md).



### 1. Pass property values as optional object arguments:

```csharp
log.Info("Welcome, {User}. You have {UnreadCount} unread messages.", "Jenny", 2);
```

Property names are inferred from placeholders in message template. 

If arguments count exceeds template placeholders count, excess arguments are named with numbers denoting their positions.

If provided arguments count is not sufficient to account for all template placeholders, the names for existing arguments are still inferred.

{% hint style="info" %}
This approach does not support multiple occurences of the same placeholder name within message template.
{% endhint %}

### 

### 2. Use a single object with named properties:

```csharp
 log.Info("Welcome, {User}. You have {UnreadCount} unread messages.", 
     new {User = "Jenny", UnreadCount = 2});
```

When using this syntax, user is responsible for making sure that object property names match the names of placeholders in message template.



### 3. Use positional placeholders:

```csharp
log.Info("Welcome, {0}. You have {1} unread messages.", "Jenny", 2);
```

Despite being somewhat deprecated nowadays, this syntax enables gradual migration from libraries that do not support structured logging.

It also supports multiple occurences of the same placeholder within a single template:

```csharp
log.Info("Welcome, {0}. {0}, you have {1} unread messages.", "Jenny", 2);
```

