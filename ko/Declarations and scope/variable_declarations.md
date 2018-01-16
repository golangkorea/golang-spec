# Variable declarations

A variable declaration creates one or more [variables](/Variables/), binds corresponding identifiers to them, and gives each a type and an initial value.

<pre>
<a id="VarDecl">VarDecl</a>     = "var" ( <a href="#VarSpec">VarSpec</a> | "(" { <a href="#VarSpec">VarSpec</a> ";" } ")" ) .
<a id="VarSpec">VarSpec</a>     = <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ( <a href="/Types/#Type">Type</a> [ "=" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> ] | "=" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> ) .
</pre>

```go
var i int
var U, V, W float64
var k = 0
var x, y float32 = -1, -2
var (
    i       int
    u, v, s = 2.0, 3.0, "bar"
)
var re, im = complexSqrt(-1)
var _, found = entries[name]  // map lookup; only interested in "found"
```

If a list of expressions is given, the variables are initialized with the expressions following the rules for [assignments](/Statements/assignments.html). Otherwise, each variable is initialized to its [zero value](/Program%20initialization%20and%20execution/the_zero_value.html).

If a type is present, each variable is given that type. Otherwise, each variable is given the type of the corresponding initialization value in the assignment. If that value is an untyped constant, it is first [converted](/Expressions/conversions.html) to its [default type](/Constants/); if it is an untyped boolean value, it is first converted to type `bool`. The predeclared value `nil` cannot be used to initialize a variable with no explicit type.

```go
var d = math.Sin(0.5)  // d is float64
var i = 42             // i is int
var t, ok = x.(T)      // t is T, ok is bool
var n = nil            // illegal
```

Implementation restriction: A compiler may make it illegal to declare a variable inside a [function body](/Declarations%20and%20scope/function_declarations.html) if the variable is never used.