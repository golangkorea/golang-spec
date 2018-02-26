# [피연산자](#operands)

피연산자는 식에 있어서 기본적인 값을 나타낸다. 피연산자는 리터럴이거나, [상수](/Declarations%20and%20scope/constant_declarations.html)를 나타내는 [blank](/Declarations%20and%20scope/blank_identifier.html) 가 아닌 ([패키지 이름을 동반할 수도 있는](/Expressions/qualified_identifiers.html)) 식별자, [변수](/Declarations%20and%20scope/variable_declarations.html), 혹은 [함수](/Declarations%20and%20scope/function_declarations.html), 함수를 생산하는 [메서드 표현식](/Expressions/method_expressions.html), 혹은 괄호친 식일 수 있다. 

[blank 식별자](/Declarations%20and%20scope/blank_identifier.html)는 할당문의 좌측에서만 피연산자로 나타날 수 있다.

<pre>
<a id="Operand">Operand</a>     = <a href="#Literal">Literal</a> | <a href="#OperandName">OperandName</a> | <a href="/Expressions/method_expressions.html#MethodExpr">MethodExpr</a> | "(" <a href="/Expressions/operators.html#Expression">Expression</a> ")" .
<a id="Literal">Literal</a>     = <a href="#BasicLit">BasicLit</a> | <a href="/Expressions/composite_literals.html#CompositeLit">CompositeLit</a> | <a href="/Expressions/function_literals.html#FunctionLit">FunctionLit</a> .
<a id="BasicLit">BasicLit</a>    = <a href="/Lexical%20elements/integer_literals.html#int_lit">int_lit</a> | <a href="/Lexical%20elements/floating-point_literals.html#float_lit">float_lit</a> | <a href="/Lexical%20elements/imaginary_literals.html#imaginary_lit">imaginary_lit</a> | <a href="/Lexical%20elements/rune_literals.html#rune_lit">rune_lit</a> | <a href="/Lexical%20elements/string_literals.html#string_lit">string_lit</a> .
<a id="OperandName">OperandName</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> | <a href="/Expressions/qualified_identifiers.html#QualifiedIdent">QualifiedIdent</a>.
</pre>
