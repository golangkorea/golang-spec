# Defer statements

A "defer" statement invokes a function whose execution is deferred to the moment the surrounding function returns, either because the surrounding function executed a [return statement](/Statements/return_statements.html), reached the end of its [function body](/Declarations%20and%20scope/function_declarations.html), or because the corresponding goroutine is [panicking](/Built-in%20functions/handling_panics.html).

<pre>
<a id="DeferStmt">DeferStmt</a> = "defer" <a href="/Expressions/operators.html#Expression">Expression</a> .
</pre>

The expression must be a function or method call; it cannot be parenthesized. Calls of built-in functions are restricted as for [expression statements](/Statements/expression_statements.html).

Each time a "defer" statement executes, the function value and parameters to the call are [evaluated as usual](/Expressions/calls.html) and saved anew but the actual function is not invoked. Instead, deferred functions are invoked immediately before the surrounding function returns, in the reverse order they were deferred. If a deferred function value evaluates to nil, execution [panics](/Built-in%20functions/handling_panics.html) when the function is invoked, not when the "defer" statement is executed.

For instance, if the deferred function is a [function literal](/Expressions/function_literals.html) and the surrounding function has [named result parameters](/Types/function_types.html) that are in scope within the literal, the deferred function may access and modify the result parameters before they are returned. If the deferred function has any return values, they are discarded when the function completes. (See also the section on [handling panics](/Built-in%20functions/handling_panics.html).)

```go
lock(l)
defer unlock(l)  // unlocking happens before surrounding function returns

// prints 3 2 1 0 before surrounding function returns
for i := 0; i <= 3; i++ {
	defer fmt.Print(i)
}

// f returns 1
func f() (result int) {
	defer func() {
		result++
	}()
	return 0
}
```