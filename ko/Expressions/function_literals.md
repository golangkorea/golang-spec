# Function literals

A function literal represents an anonymous [function](/Declarations%20and%20scope/function_declarations.html).

<pre>
<a id="FunctionLit">FunctionLit</a> = "func" <a href="/Declarations%20and%20scope/function_declarations.html#Function">Function</a> .
</pre>

```
func(a, b int, z float64) bool { return a*b < int(z) }
```

A function literal can be assigned to a variable or invoked directly.

```
f := func(x, y int) int { return x + y }
func(ch chan int) { ch <- ACK }(replyChan)
```

Function literals are *closures*: they may refer to variables defined in a surrounding function. Those variables are then shared between the surrounding function and the function literal, and they survive as long as they are accessible.