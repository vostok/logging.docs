# Special properties

Here's the list of all special properties supported by [output templates](output-templates.md):

* `Timestamp` — emits log event timestamp. Supports [format specifiers](format-specifiers.md).

  * Example output: `2019-03-11 19:21:52,755`

* `Level` — emits log event level. Supports a number of special [format specifiers](format-specifiers.md).

  * Example output: `INFO`

* `Message` — emits rendered log event message \([template](../syntax/message-templates.md) with substituted placeholders\).

  * Example output: `Hello, world!`

* `Exception` — prints event's exception along with its stack trace and inner exceptions.

* `NewLine` — emits a platform-dependent newline.

* `Uptime` — emits the number of milliseconds elapsed since application start. Supports [format specifiers](format-specifiers.md).

* `Properties` — emits all properties not mentioned elsewhere in the output template as a JSON object.
  * Example output: `{`"prop1": "value1", "prop2" : "value2"`}`

