# Go statements

A "go" statement starts the execution of a function call as an independent concurrent thread of control, or goroutine, within the same address space.

<pre>
<a id="GoStmt">GoStmt</a> = "go" <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

The expression must be a function or method call; it cannot be parenthesized. Calls of built-in functions are restricted as for [expression statements](/Statements/expression_statements.html).

The function value and parameters are [evaluated as usual](/Expressions/calls.html) in the calling goroutine, but unlike with a regular call, program execution does not wait for the invoked function to complete. Instead, the function begins executing independently in a new goroutine. When the function terminates, its goroutine also terminates. If the function has any return values, they are discarded when the function completes.

```
go Server()
go func(ch chan<- bool) { for { sleep(10); ch <- true }} (c)
```