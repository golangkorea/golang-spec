# [라벨이 붙은 구문](#labeled-statements)

라벨이 붙은 구문은 `goto`, `break`, `continue` 문의 대상이 될 수 있다.

<pre>
<a id="LabeledStmt">LabeledStmt</a> = <a href="#Label">Label</a> ":" <a href="/Statements/#Statement">Statement</a> .
<a id="Label">Label</a>       = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
</pre>

```go
Error: log.Panic("error encountered")
```
