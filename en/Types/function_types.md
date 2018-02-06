# [Function types](#function-types)

A function type denotes the set of all functions with the same parameter and result types. The value of an uninitialized variable of function type is `nil`.

<pre>
<a id="FunctionType">FunctionType</a>   = "func" <a href="#Signature">Signature</a> .
<a id="Signature">Signature</a>      = <a href="#Parameters">Parameters</a> [ <a href="#Result">Result</a> ] .
<a id="Result">Result</a>         = <a href="#Parameters">Parameters</a> | <a href="/Types/#Type">Type</a> .
<a id="Parameters">Parameters</a>     = "(" [ <a href="#ParameterList">ParameterList</a> [ "," ] ] ")" .
<a id="ParameterList">ParameterList</a>  = <a href="#ParameterDecl">ParameterDecl</a> { "," <a href="#ParameterDecl">ParameterDecl</a> } .
<a id="ParameterDecl">ParameterDecl</a>  = [ <a href="/Declarations%20and%20scope/constant_declarations.html#IdentifierList">IdentifierList</a> ] [ "..." ] <a href="/Types/#Type">Type</a> .
</pre>

Within a list of parameters or results, the names (IdentifierList) must either all be present or all be absent. If present, each name stands for one item (parameter or result) of the specified type and all non-[blank](/Declarations%20and%20scope/blank_identifier.html) names in the signature must be [unique](/Declarations%20and%20scope/uniqueness_of_identifiers.html). If absent, each type stands for one item of that type. Parameter and result lists are always parenthesized except that if there is exactly one unnamed result it may be written as an unparenthesized type.

The final incoming parameter in a function signature may have a type prefixed with `...`. A function with such a parameter is called *variadic* and may be invoked with zero or more arguments for that parameter.

```go
func()
func(x int) int
func(a, _ int, z float32) bool
func(a, b int, z float32) (bool)
func(prefix string, values ...int)
func(a, b int, z float64, opt ...interface{}) (success bool)
func(int, int, float64) (float64, *[]int)
func(n int) func(p *T)
```
