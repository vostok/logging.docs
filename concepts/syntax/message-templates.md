# Message templates

Message template is the text of a log message that can potentially contain placeholders filled with property values during rendering.

Placeholders are always specified in curly brackets: `Response code = {Code}.`

During rendering, placeholders are replaced with values of properties with corresponding names:

`Response code = {Code}` + `{"Code": "200"}` = `Response code = 200`

Any mismatched brackets are kept as-is: `{key}` template renders to the same text.

Any placeholders without corresponding properties are replaced with empty strings.

Double curly brackets can be used to escape occurrences of curly brackets in text: `{{key}}` template renders to `{key}` text.

{% hint style="warning" %}
Do not use message instead of message template

For example, instead of `log.Info(json)` you should use `log.Info("{Json}", json)`.

Otherwise, you may have performance issues (due to internal templates cache) or corrupted messages (due to rendering stage).
{% endhint %}
