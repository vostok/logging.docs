# Format specifiers

[Output templates](output-templates.md) support providing format specifiers for properties after a semicolon: `{prop:format}`.

There's generic support for `IFormattable` values that allows to use format specifiers defined for standard primitives \(numeric types, `TimeSpan`, `DateTime`, etc.\) as well as customize rendering of custom complex types.

Here are some basic examples of property formats: 

* `{Timestamp:yy-mm-dd}`
* `{RandomDouble:0.###}`



### Special formats

#### Whitespace insertion

Ordinary properties can be augmented with one of three special formats to insert surrounding whitespaces:

* `W` — inserts a leading whitespace next to property value.
* `w` — inserts a trailing whitespace next to property value.
* `wW` — inserts both leading and trailing whitespaces next to property value.

Note that no whitespaces are inserted when there's no property with given name in log event. This allows to chain multiple optional properties in the output template and avoid having multiples in rendered message spaces when none of these properties are present.

#### Log level formats

Special `Level` property in output templates supports custom formats consisting of case and width.

Allowed  case specifiers are `u` \(uppercase\), `w` \(lowercase\) and `t` \(title case\).

Allowed width ranges from 1 to 5.

Here's how the `Error` value is rendered with different level formats:

* `u5` --&gt; `ERROR`
* `u3` --&gt; `ERR`
* `w5` --&gt; `error`
* `w3` --&gt; `err`
* `t5` --&gt; `Error`
* `t3` --&gt; `Err`  

