# [기본 식](#primary-expressions)

기본 식은 단항 식과 이항 식의 피연산자다.

<pre>
<a id="PrimaryExpr">PrimaryExpr</a> =
    <a href="/Expressions/operands.html#Operand">Operand</a> |
    <a href="/Expressions/conversions.html#Conversion">Conversion</a> |
    <a href="#PrimaryExpr">PrimaryExpr</a> <a href="#Selector">Selector</a> |
    <a href="#PrimaryExpr">PrimaryExpr</a> <a href="#Index">Index</a> |
    <a href="#PrimaryExpr">PrimaryExpr</a> <a href="#Slice">Slice</a> |
    <a href="#PrimaryExpr">PrimaryExpr</a> <a href="#TypeAssertion">TypeAssertion</a> |
    <a href="#PrimaryExpr">PrimaryExpr</a> <a href="#Arguments">Arguments</a> .

<a id="Selector">Selector</a>       = "." <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> .
<a id="Index">Index</a>          = "[" <a href="/Expressions/operators.html#Expression">Expression</a> "]" .
<a id="Slice">Slice</a>          = "[" [ <a href="/Expressions/operators.html#Expression">Expression</a> ] ":" [ <a href="/Expressions/operators.html#Expression">Expression</a> ] "]" |
                 "[" [ <a href="/Expressions/operators.html#Expression">Expression</a> ] ":" <a href="/Expressions/operators.html#Expression">Expression</a> ":" <a href="/Expressions/operators.html#Expression">Expression</a> "]" .
<a id="TypeAssertion">TypeAssertion</a>  = "." "(" <a href="/Types/#Type">Type</a> ")" .
<a id="Arguments">Arguments</a>      = "(" [ ( <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> | <a href="/Types/#Type">Type</a> [ "," <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> ] ) [ "..." ] [ "," ] ] ")" .
</pre>

```go
x
2
(s + ".txt")
f(3.1415, true)
Point{1, 2}
m["foo"]
s[i : j + 1]
obj.color
f.p[i].x()
```
