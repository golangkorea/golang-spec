# [Identifiers](#identifiers)

Identifiers name program entities such as variables and types. An identifier is a sequence of one or more letters and digits. The first character in an identifier must be a letter.

<pre>
<a id="identifier">identifier</a> = <a href="/Source code representation/letters_and_digits.html#letter">letter</a> { <a href="/Source code representation/letters_and_digits.html#letter">letter</a> | <a href="/Source code representation/characters.html#unicode_digit">unicode_digit</a> } .
</pre>

```go
a
_x9
ThisVariableIsExported
αβ
```

Some identifiers are [predeclared](/Declarations%20and%20scope/predeclared_identifiers.html).
