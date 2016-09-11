# Variable declarations

A variable declaration creates one or more variables, binds corresponding identifiers to them, and gives each a type and an initial value.

<pre>
VarDecl     = "var" ( VarSpec | "(" { VarSpec ";" } ")" ) .
VarSpec     = IdentifierList ( Type [ "=" ExpressionList ] | "=" ExpressionList ) .
</pre>

```
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

If a list of expressions is given, the variables are initialized with the expressions following the rules for assignments. Otherwise, each variable is initialized to its zero value.

If a type is present, each variable is given that type. Otherwise, each variable is given the type of the corresponding initialization value in the assignment. If that value is an untyped constant, it is first converted to its default type; if it is an untyped boolean value, it is first converted to type bool. The predeclared value nil cannot be used to initialize a variable with no explicit type.

```
var d = math.Sin(0.5)  // d is float64
var i = 42             // i is int
var t, ok = x.(T)      // t is T, ok is bool
var n = nil            // illegal
```

Implementation restriction: A compiler may make it illegal to declare a variable inside a function body if the variable is never used.