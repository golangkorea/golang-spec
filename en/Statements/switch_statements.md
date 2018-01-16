# Switch statements

"Switch" statements provide multi-way execution. An expression or type specifier is compared to the "cases" inside the "switch" to determine which branch to execute.

<pre>
<a id="SwitchStmt">SwitchStmt</a> = <a href="#ExprSwitchStmt">ExprSwitchStmt</a> | <a href="#TypeSwitchStmt">TypeSwitchStmt</a> .
</pre>

There are two forms: expression switches and type switches. In an expression switch, the cases contain expressions that are compared against the value of the switch expression. In a type switch, the cases contain types that are compared against the type of a specially annotated switch expression. The switch expression is evaluated exactly once in a switch statement.

## Expression switches

In an expression switch, the switch expression is evaluated and the case expressions, which need not be constants, are evaluated left-to-right and top-to-bottom; the first one that equals the switch expression triggers execution of the statements of the associated case; the other cases are skipped. If no case matches and there is a "default" case, its statements are executed. There can be at most one default case and it may appear anywhere in the "switch" statement. A missing switch expression is equivalent to the boolean value true.

<pre>
<a id="ExprSwitchStmt">ExprSwitchStmt</a> = "switch" [ <a href="/Statements/#SimpleStmt">SimpleStmt</a> ";" ] [ <a href="/Expressions/operators.html#Expression">Expression</a> ] "{" { <a href="#ExprCaseClause">ExprCaseClause</a> } "}" .
<a id="ExprCaseClause">ExprCaseClause</a> = <a href="#ExprSwitchCase">ExprSwitchCase</a> ":" <a href="/Blocks/#StatementList">StatementList</a> .
<a id="ExprSwitchCase">ExprSwitchCase</a> = "case" <a href="/Declarations%20and%20scope/constant_declarations.html#ExpressionList">ExpressionList</a> | "default" .
</pre>

If the switch expression evaluates to an untyped constant, it is first [converted](/Expressions/conversions.html) to its [default type](/Constants/); if it is an untyped boolean value, it is first converted to type `bool`. The predeclared untyped value `nil` cannot be used as a switch expression.

If a case expression is untyped, it is first [converted](/Expressions/conversions.html) to the type of the switch expression. For each (possibly converted) case expression x and the value t of the switch expression, x == t must be a valid [comparison](/Expressions/comparison_operators.html).

In other words, the switch expression is treated as if it were used to declare and initialize a temporary variable t without explicit type; it is that value of t against which each case expression x is tested for equality.

In a case or default clause, the last non-empty statement may be a (possibly [labeled](/Statements/labeled_statements.html)) ["fallthrough" statement](/Statements/fallthrough_statements.html) to indicate that control should flow from the end of this clause to the first statement of the next clause. Otherwise control flows to the end of the "switch" statement. A "fallthrough" statement may appear as the last statement of all but the last clause of an expression switch.

The switch expression may be preceded by a simple statement, which executes before the expression is evaluated.

```go
switch tag {
default: s3()
case 0, 1, 2, 3: s1()
case 4, 5, 6, 7: s2()
}

switch x := f(); {  // missing switch expression means "true"
case x < 0: return -x
default: return x
}

switch {
case x < y: f1()
case x < z: f2()
case x == 4: f3()
}
```

Implementation restriction: A compiler may disallow multiple case expressions evaluating to the same constant. For instance, the current compilers disallow duplicate integer, floating point, or string constants in case expressions.

## Type switches

A type switch compares types rather than values. It is otherwise similar to an expression switch. It is marked by a special switch expression that has the form of a [type assertion](/Expressions/type_assertions.html) using the reserved word type rather than an actual type:

```go
switch x.(type) {
// cases
}
```

Cases then match actual types T against the dynamic type of the expression x. As with type assertions, x must be of [interface type](/Types/interface_types.html), and each non-interface type T listed in a case must implement the type of x. The types listed in the cases of a type switch must all be [different](/Properties%20of%20types%20and%20values/type_identity.html).

<pre>
<a id="TypeSwitchStmt">TypeSwitchStmt</a>  = "switch" [ <a href="/Statements/#SimpleStmt">SimpleStmt</a> ";" ] <a href="#TypeSwitchGuard">TypeSwitchGuard</a> "{" { <a href="#TypeCaseClause">TypeCaseClause</a> } "}" .
<a id="TypeSwitchGuard">TypeSwitchGuard</a> = [ <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> ":=" ] <a href="/Expressions/primary_expressions.html#PrimaryExpr">PrimaryExpr</a> "." "(" "type" ")" .
<a id="TypeCaseClause">TypeCaseClause</a>  = <a href="#TypeSwitchCase">TypeSwitchCase</a> ":" <a href="/Blocks/#StatementList">StatementList</a> .
<a id="TypeSwitchCase">TypeSwitchCase</a>  = "case" <a href="#TypeList">TypeList</a> | "default" .
<a id="TypeList">TypeList</a>        = <a href="/Types/#Type">Type</a> { "," <a href="/Types/#Type">Type</a> } .
</pre>

The TypeSwitchGuard may include a [short variable declaration](/Declarations%20and%20scope/short_variable_declarations.html). When that form is used, the variable is declared at the beginning of the [implicit block](/Blocks/) in each clause. In clauses with a case listing exactly one type, the variable has that type; otherwise, the variable has the type of the expression in the TypeSwitchGuard.

The type in a case may be [nil](/Declarations%20and%20scope/predeclared_identifiers.html); that case is used when the expression in the TypeSwitchGuard is a nil interface value. There may be at most one nil case.

Given an expression x of type interface{}, the following type switch:

```go
switch i := x.(type) {
case nil:
	printString("x is nil")                // type of i is type of x (interface{})
case int:
	printInt(i)                            // type of i is int
case float64:
	printFloat64(i)                        // type of i is float64
case func(int) float64:
	printFunction(i)                       // type of i is func(int) float64
case bool, string:
	printString("type is bool or string")  // type of i is type of x (interface{})
default:
	printString("don't know the type")     // type of i is type of x (interface{})
}
```

could be rewritten:

```go
v := x  // x is evaluated exactly once
if v == nil {
	i := v                                 // type of i is type of x (interface{})
	printString("x is nil")
} else if i, isInt := v.(int); isInt {
	printInt(i)                            // type of i is int
} else if i, isFloat64 := v.(float64); isFloat64 {
	printFloat64(i)                        // type of i is float64
} else if i, isFunc := v.(func(int) float64); isFunc {
	printFunction(i)                       // type of i is func(int) float64
} else {
	_, isBool := v.(bool)
	_, isString := v.(string)
	if isBool || isString {
		i := v                         // type of i is type of x (interface{})
		printString("type is bool or string")
	} else {
		i := v                         // type of i is type of x (interface{})
		printString("don't know the type")
	}
}
```

The type switch guard may be preceded by a simple statement, which executes before the guard is evaluated.

The "fallthrough" statement is not permitted in a type switch.