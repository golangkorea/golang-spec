# Return statements

A "return" statement in a function F terminates the execution of F, and optionally provides one or more result values. Any functions deferred by F are executed before F returns to its caller.

<pre>
<a id="ReturnStmt">ReturnStmt</a> = "return" [ <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> ] .
</pre>

In a function without a result type, a "return" statement must not specify any result values.

```go
func noResult() {
    return
}
```

There are three ways to return values from a function with a result type:

  1. The return value or values may be explicitly listed in the "return" statement. Each expression must be single-valued and [assignable](/Properties%20of%20types%20and%20values/assignability.html) to the corresponding element of the function's result type.
    <pre>
func simpleF() int {
    return 2
}
&nbsp;
func complexF1() (re float64, im float64) {
    return -7.0, -4.0
}
    </pre>
  2. The expression list in the "return" statement may be a single call to a multi-valued function. The effect is as if each value returned from that function were assigned to a temporary variable with the type of the respective value, followed by a "return" statement listing these variables, at which point the rules of the previous case apply.
    <pre>
func complexF2() (re float64, im float64) {
    return complexF1()
}
    </pre>
  3. The expression list may be empty if the function's result type specifies names for its [result parameters](/Types/function_types.html). The result parameters act as ordinary local variables and the function may assign values to them as necessary. The "return" statement returns the values of these variables.
    <pre>
func complexF3() (re float64, im float64) {
    re = 7.0
    im = 4.0
    return
}
&nbsp;
func (devnull) Write(p []byte) (n int, _ error) {
    n = len(p)
    return
}
    </pre>

Regardless of how they are declared, all the result values are initialized to the [zero values](/Program%20initialization%20and%20execution/the_zero_value.html) for their type upon entry to the function. A "return" statement that specifies results sets the result parameters before any deferred functions are executed.

Implementation restriction: A compiler may disallow an empty expression list in a "return" statement if a different entity (constant, type, or variable) with the same name as a result parameter is in [scope](/Declarations%20and%20scope/) at the place of the return.

```go
func f(n int) (res int, err error) {
    if _, err := f(n-1); err != nil {
        return  // invalid return statement: err is shadowed
    }
    return
}
```