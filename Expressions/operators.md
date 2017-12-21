# [연산자(Operators)](#operators)

* Go 버전: 1.9
* 원문: [Operators](https://golang.org/ref/spec#Operators)
* 번역자: Jhonghee Park (@jhonghee)

Operators combine operands into expressions.

연산자는 피연산자들을 조합해서 식(expression)으로 만든다.

<pre>
<a id="Expression">Expression</a> = <a href="#UnaryExpr">UnaryExpr</a> | <a href="#Expression">Expression</a> <a href="#binary_op">binary_op</a> <a href="#Expression">Expression</a> .
<a id="UnaryExpr">UnaryExpr</a>  = <a href="/Expressions/primary_expressions.html#PrimaryExpr">PrimaryExpr</a> | <a href="#unary_op">unary_op</a> <a href="#UnaryExpr">UnaryExpr</a> .

<a id="binary_op">binary_op</a>  = "||" | "&&" | <a href="#rel_op">rel_op</a> | <a href="#add_op">add_op</a> | <a href="#mul_op">mul_op</a> .
<a id="rel_op">rel_op</a>     = <code>"==" | "!=" | "<" | "<=" | ">" | ">="</code> .
<a id="add_op">add_op</a>     = <code>"+" | "-" | "|" | "^"</code>
<a id="unary_op">unary_op</a>   = <code>"+" | "-" | "!" | "^" | "*" | "&" | "<-"</code> .
</pre>

Comparisons are discussed [elsewhere](/Expressions/comparison_operators.html). For other binary operators, the operand types must be [identical](/Properties%20of%20types%20and%20values/type_identity.html) unless the operation involves shifts or untyped [constants](/Constants/). For operations involving constants only, see the section on [constant expressions](/Expressions/constant_expressions.html).

비교연산은 [별도의 섹션](/Expressions/comparison_operators.html)에서 다루고 있다. 이항 연산자들(binary operators)에 대해서는, 시프트(shifts)연산이나 미지정 타입 [상수](/Constants/)를 동반한 연산이 아닌 경우 피연산자의 타입이 [같아야](/Properties%20of%20types%20and%20values/type_identity.html) 한다. 상수만 관련된 연산들은 [상수 식](/Expressions/constant_expressions.html) 섹션을 참고하라.

Except for shift operations, if one operand is an untyped [constant](/Constants/) and the other operand is not, the constant is [converted](/Expressions/conversions.html) to the type of the other operand.

한 쪽 피연산자가 미지정 타입의 [상수](/Constants/)이고 다른 쪽 피연산자는 타입 상수라면, 이 상수는 다른 쪽 피연산자의 타입에 맞게 [변환](/Expressions/conversions.html)된다. 시프트 연산에는 이 규칙이 적용되지 않는다.

The right operand in a shift expression must have unsigned integer type or be an untyped constant representable by a value of type `unit`. If the left operand of a non-constant shift expression is an untyped constant, it is first converted to the type it would assume if the shift expression were replaced by its left operand alone.

시프트 식의 오른쪽 피연산자는 부호 없는 정수 타입이거나 `unit` 타입의 값으로 표현할 수 있는 미지정 타입의 상수여야 한다. 시프트 식에 상수가 아닌 피연산자가 포함되어 있고, 왼쪽 피연산자가 미지정 타입의 상수라면, 왼쪽 피연산자만 사용되었을 때처럼 타입 변환이 발생한다. 즉, 전체 시프트 식이 왼쪽 피연산자로 대체된 것과 같은 효과가 나타난다.

```
var s uint = 33
var i = 1<<s           // 1 has type int
var j int32 = 1<<s     // 1 has type int32; j == 0
var k = uint64(1<<s)   // 1 has type uint64; k == 1<<33
var m int = 1.0<<s     // 1.0 has type int; m == 0 if ints are 32bits in size
var n = 1.0<<s == j    // 1.0 has type int32; n == true
var o = 1<<s == 2<<s   // 1 and 2 have type int; o == true if ints are 32bits in size
var p = 1<<s == 1<<33  // illegal if ints are 32bits in size: 1 has type int, but 1<<33 overflows int
var u = 1.0<<s         // illegal: 1.0 has type float64, cannot shift
var u1 = 1.0<<s != 0   // illegal: 1.0 has type float64, cannot shift
var u2 = 1<<s != 1.0   // illegal: 1 has type float64, cannot shift
var v float32 = 1<<s   // illegal: 1 has type float32, cannot shift
var w int64 = 1.0<<33  // 1.0<<33 is a constant shift expression
```

```
var s uint = 33
var i = 1<<s           // 1은 int 타입이다.
var j int32 = 1<<s     // 1은 int32 타입이다; j == 0
var k = uint64(1<<s)   // 1은 uint64 타입이다; k == 1<<33
var m int = 1.0<<s     // 1.0은 int 타입이다; int 타입의 크기가 32비트라면 m == 0
var n = 1.0<<s == j    // 1.0은 int32 타입이다; n == true
var o = 1<<s == 2<<s   // 1과 2의 int; int 타입의 크기가 32bit라면 o == true
var p = 1<<s == 1<<33  // int 타입의 크기가 32bit라면 허용되지 않음: 1은 int 타입이지만 1<<33 연산이 int 타입의 크기를 오버플로우하기 때문에 허용되지 않는다.
var u = 1.0<<s         // 허용않됨: 1.0은 float64 타입이며, 시프트할 수 없다
var u1 = 1.0<<s != 0   // 허용않됨: 1.0은 float64 타입이며, 시프트할 수 없다
var u2 = 1<<s != 1.0   // 허용않됨: 1은 float64 타입이며, 시프트할 수 없다
var v float32 = 1<<s   // 허용않됨: 1은 float32 타입이며, 시프트할 수 없다
var w int64 = 1.0<<33  // 1.0<<33은 상수 시프트 식이다
```

## Operator precedence

## 연산자 우선 순위

Unary operators have the highest precedence. As the ++ and -- operators form statements, not expressions, they fall outside the operator hierarchy. As a consequence, statement *p++ is the same as (*p)++.

단항 연산자들은 가장 높은 우선 순위를 가진다. `++`와 `--` 연산자들은 식(expressions)이 아닌 구문(statements)을 형성하기 때문에, 연산자 우선순위에 포함시키지 않는다. 그 결과, 구문 `*p++`는 `(*p)++`과 같다. 

There are five precedence levels for binary operators. Multiplication operators bind strongest, followed by addition operators, comparison operators, && (logical AND), and finally || (logical OR):

이항 연산자들에게는 5개의 우선 순위가 있다. 곱셈 연산자들의 우선 순위가 높고 다음은 덧셈 연산자, 비교 연산자, `&&` (논리 연산자 AND), `||` (논리 연산자 OR) 순이다:

```
Precedence    Operator
    5             *  /  %  <<  >>  &  &^
    4             +  -  |  ^
    3             ==  !=  <  <=  >  >=
    2             &&
    1             ||
```

Binary operators of the same precedence associate from left to right. For instance, x / y * z is the same as (x / y) * z.

우선 순위가 같은 이항 연산자들 간의 우선 순위는 보다 왼쪽에 위치한 연산자일수록 더 높다. 예를 들어, `x / y * z`은 `(x / y) * z`와 같다.

```
+x
23 + 3*x[i]
x <= f()
^a >> b
f() || g()
x == y+1 && <-chanPtr > 0
```
