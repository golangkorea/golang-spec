# Operands

Operands denote the elementary values in an expression. An operand may be a literal, a (possibly [qualified](/Expressions/qualified_identifiers.html)) non-[blank](/Declarations%20and%20scope/blank_identifier.html) identifier denoting a [constant](/Declarations%20and%20scope/constant_declarations.html), [variable](/Declarations%20and%20scope/variable_declarations.html), or [function](/Declarations%20and%20scope/function_declarations.html), a [method expression](/Expressions/method_expressions.html) yielding a function, or a parenthesized expression.

The [blank identifier](/Declarations%20and%20scope/blank_identifier.html) may appear as an operand only on the left-hand side of an assignment.

<pre>
<a id="Operand">Operand</a>     = <a href="#Literal">Literal</a> | <a href="#OperandName">OperandName</a> | MethodExpr | "(" Expression ")" .
<a id="Literal">Literal</a>     = <a href="#BasicLit">BasicLit</a> | CompositeLit | FunctionLit .
<a id="BasicLit">BasicLit</a>    = int_lit | float_lit | imaginary_lit | rune_lit | string_lit .
<a id="OperandName">OperandName</a> = identifier | QualifiedIdent.
</pre>
