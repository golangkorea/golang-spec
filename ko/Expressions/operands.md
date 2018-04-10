# [피연산자](#operands)

피연산자는 식에서 기본적인 값을 나타낸다. 피연산자로 리터럴, [상수](/Declarations%20and%20scope/constant_declarations.html)를 나타내는 [blank](/Declarations%20and%20scope/blank_identifier.html) 식별자가 아닌 식별자 ([한정적 식별자도 가능](/Expressions/qualified_identifiers.html)), [변수](/Declarations%20and%20scope/variable_declarations.html), [함수](/Declarations%20and%20scope/function_declarations.html), 결괏값이 함수인 [메서드 식](/Expressions/method_expressions.html), 괄호로 묶은 식을 사용할 수 있다. 

[blank 식별자](/Declarations%20and%20scope/blank_identifier.html)는 할당 문의 좌측에서만 피연산자로 나타날 수 있다.

<pre>
<a id="Operand">Operand</a>     = <a href="#Literal">Literal</a> | <a href="#OperandName">OperandName</a> | <a href="/Expressions/method_expressions.html#MethodExpr">MethodExpr</a> | "(" <a href="/Expressions/operators.html#Expression">Expression</a> ")" .
<a id="Literal">Literal</a>     = <a href="#BasicLit">BasicLit</a> | <a href="/Expressions/composite_literals.html#CompositeLit">CompositeLit</a> | <a href="/Expressions/function_literals.html#FunctionLit">FunctionLit</a> .
<a id="BasicLit">BasicLit</a>    = <a href="/Lexical%20elements/integer_literals.html#int_lit">int_lit</a> | <a href="/Lexical%20elements/floating-point_literals.html#float_lit">float_lit</a> | <a href="/Lexical%20elements/imaginary_literals.html#imaginary_lit">imaginary_lit</a> | <a href="/Lexical%20elements/rune_literals.html#rune_lit">rune_lit</a> | <a href="/Lexical%20elements/string_literals.html#string_lit">string_lit</a> .
<a id="OperandName">OperandName</a> = <a href="/Lexical%20elements/identifiers.html#identifier">identifier</a> | <a href="/Expressions/qualified_identifiers.html#QualifiedIdent">QualifiedIdent</a>.
</pre>
