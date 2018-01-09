# If statements

"If" statements specify the conditional execution of two branches according to the value of a boolean expression. If the expression evaluates to true, the "if" branch is executed, otherwise, if present, the "else" branch is executed.

<pre>
<a id="IfStmt">IfStmt</a> = "if" [ <a href="/Statements/#SimpleStmt">SimpleStmt</a> ";" ] <a href="/Expressions/operators.html#Expression">Expression</a> <a href="/Blocks/#Block">Block</a> [ "else" ( <a href="#IfStmt">IfStmt</a> | <a href="/Blocks/#Block">Block</a> ) ] .
</pre>

```go
if x > max {
    x = max
}
```

The expression may be preceded by a simple statement, which executes before the expression is evaluated.

```go
if x := f(); x < y {
    return x
} else if x > z {
    return z
} else {
    return y
}
```