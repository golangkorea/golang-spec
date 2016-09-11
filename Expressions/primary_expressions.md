# Primary expressions

Primary expressions are the operands for unary and binary expressions.

<pre>
<a id="PrimaryExpr">PrimaryExpr</a> =
	Operand |
	Conversion |
	PrimaryExpr Selector |
	PrimaryExpr Index |
	PrimaryExpr Slice |
	PrimaryExpr TypeAssertion |
	PrimaryExpr Arguments .

<a id="Selector">Selector</a>       = "." identifier .
<a id="Index">Index</a>          = "[" Expression "]" .
<a id="Slice">Slice</a>          = "[" [ Expression ] ":" [ Expression ] "]" |
                 "[" [ Expression ] ":" Expression ":" Expression "]" .
<a id="TypeAssertion">TypeAssertion</a>  = "." "(" Type ")" .
<a id="Arguments">Arguments</a>      = "(" [ ( ExpressionList | Type [ "," ExpressionList ] ) [ "..." ] [ "," ] ] ")" .
</pre>

```
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