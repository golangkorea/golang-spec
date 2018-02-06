# [Run-time panics](#run-time-panics)

Execution errors such as attempting to index an array out of bounds trigger a *run-time panic* equivalent to a call of the built-in function [panic](/Built-in%20functions/handling_panics.html) with a value of the implementation-defined interface type `runtime.Error`. That type satisfies the predeclared interface type [error](/Errors/). The exact error values that represent distinct run-time error conditions are unspecified.

```go
package runtime

type Error interface {
	error
	// and perhaps other methods
}
```
