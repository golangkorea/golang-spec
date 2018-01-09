# Operands

Operands denote the elementary values in an expression. An operand may be a literal, a (possibly [qualified](/Expressions/qualified_identifiers.html)) non-[blank](/Declarations%20and%20scope/blank_identifier.html) identifier denoting a [constant](/Declarations%20and%20scope/constant_declarations.html), [variable](/Declarations%20and%20scope/variable_declarations.html), or [function](/Declarations%20and%20scope/function_declarations.html), a [method expression](/Expressions/method_expressions.html) yielding a function, or a parenthesized expression.

The [blank identifier](/Declarations%20and%20scope/blank_identifier.html) may appear as an operand only on the left-hand side of an assignment.

<pre>
<a id="Operand">Operand</a>     = <a href="#Literal">Literal</a> | <a href="#OperandName">OperandName</a> | <a href="/Expressions/method_expressions.html#MethodExpr">MethodExpr</a> | "(" <a href="/Expressions/operators.html#Expression">Expression</a> ")" .
<a id="Literal">Literal</a>     = <a href="#BasicLit">BasicLit</a> | <a href="/Expressions/composite_literals.html#CompositeLit">CompositeLit</a> | <a href="/Expressions/function_literals.html#FunctionLit">FunctionLit</a> .
<a id="BasicLit">BasicLit</a>    = <a href="/Lexical%20elements/integer_literals.html#int_lit">int_lit</a> | <a href="/Lexical%20elements/floating-point_literals.html#float_lit">float_lit</a> | <a href="/Lexical%20elements/imaginary_literals.html#imaginary_lit">imaginary_lit</a> | <a href="/Lexical%20elements/rune_literals.html#rune_lit">rune_lit</a> | <a href="/Lexical%20elements/string_literals.html#string_lit">string_lit</a> .
<a id="OperandName">OperandName</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> | <a href="/Expressions/qualified_identifiers.html#QualifiedIdent">QualifiedIdent</a>.
</pre>