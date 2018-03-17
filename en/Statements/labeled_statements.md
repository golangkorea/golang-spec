# [Labeled statements](#labeled-statements)

A labeled statement may be the target of a `goto`, `break` or `continue` statement.

<pre>
<a id="LabeledStmt">LabeledStmt</a> = <a href="#Label">Label</a> ":" <a href="/Statements/#Statement">Statement</a> .
<a id="Label">Label</a>       = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
</pre>

```go
Error: log.Panic("error encountered")
```
